---
title: 记一次前端国际化
date: 2020-4-1
author: leonliu
category: JS
tags:
- JS
---

# React项目国际化
## 背景问题及带来思考
<!--more-->
### 1.语言翻译
- 项目前期建立时,仅考虑支持中文,未考虑支持多语言版本(前期决策很关键,对一个旧工程做国际化改造是十分痛苦的)
- 翻译方式: 手动翻译(准确性高,但是耗时)、 借助开放平台跑自动化脚本(准确性和语义会打一定折扣,效率高)

### 2.map表维护
- 一个文件维护(文件太大, 可能会对页面加载速率带来一定影响, 但是对于自动化脚本翻译方便)
- 多个文件维护(拆发了词表, 并根据页面动态加载词表, 对页面加载友好, 但是可能会增大维护成本, 自动化脚本处理也会带来一定问题)

### 3.样式问题
- 不同语言的文本长度不一样会造成样式错乱(这里暂时未处理)

## 解决方案
### 集成react-intl

[react-intl详细代码](https://github.com/lord2416/leon-cli)

例子:

```
import React from 'react'
import ReactDOM from 'react-dom'
import {injectIntl, IntlProvider, FormattedRelative} from 'react-intl'

const PostDate = injectIntl(({date, intl}) => (
  <span title={intl.formatDate(date)}>
    <FormattedRelative value={date} />
  </span>
))

const App = ({post}) => (
  <div>
    <h1>{post.title}</h1>
    <p>
      <PostDate date={post.date} />
    </p>
    <div>{post.body}</div>
  </div>
)

ReactDOM.render(
  <IntlProvider locale={navigator.language}>
    <App
      post={{
        title: 'Hello, World!',
        date: new Date(1459913574887),
        body: 'Amazing content.',
      }}
    />
  </IntlProvider>,
  document.getElementById('container')
)
```
react-intl本身不支持动态加载, 我们需要自己实现

### 基于react-intl的动态加载高阶组件实现
```
import React, { PureComponent, Fragment } from 'react';
import { connect } from 'dva';
import { IntlProvider, injectIntl } from 'react-intl';

const IntlMap = {
  zh_CN: 'zh',
  en_US: 'en',
  th_TH: 'th',
};

@connect(({ global }) => ({ global }))
export class DynamicWrapperIntl extends PureComponent {
  state = {
    data: null,
  };

  componentDidMount() {
    this.resolveImport();
  }

  componentDidUpdate(prevProps) {
    if (prevProps.global.langs !== this.props.global.langs) {
      this.resolveImport();
    }
  }

  resolveImport = () => {
    const { global: { langs = 'zh_CN' }, name } = this.props;
    if (typeof name === 'string') {
      import(`../../locale/${langs}/${name}`)
        .then(m => {
          // console.log('DynamicWrapperIntl:', m.default);
          this.setState({
            data: m.default,
          });
        })
        .catch(e => {
          console.log('DynamicWrapperIntl:', e);
        });
    } else if (name instanceof Array) {
      Promise.all(name.map(i => import(`../../locale/${langs}/${i}`)))
        .then(m => {
          const data = m.reduce((acc, cur) => {
            acc = {
              ...acc,
              ...cur.default,
            };
            return acc;
          }, {});
          this.setState({
            data,
          });
        })
        .catch(e => {
          console.log('DynamicWrapperIntl:', e);
        });
    }
  };

  render() {
    const { global: { langs = 'zh_CN' } } = this.props;
    const { data } = this.state;

    return (
      <Fragment>
        {data && (
          <IntlProvider locale={IntlMap[langs]} messages={data}>
            {this.props.children({
              langs,
              locales: data,
            })}
          </IntlProvider>
        )}
      </Fragment>
    );
  }
}

export const withDynamicWrapperIntl = (name, setting = {}) => WrapperComponent => {
  const Wrapper = withInjectIntl(setting)(WrapperComponent);
  return class DynamicWrapperIntlHoc extends PureComponent {
    render() {
      return (
        <DynamicWrapperIntl name={name}>
          {wrapperProps => <Wrapper {...this.props} {...wrapperProps} />}
        </DynamicWrapperIntl>
      );
    }
  };
};

export const withInjectIntl = (setting = {}) => WrapperComponent =>
  injectIntl(WrapperComponent, setting);
```

### 基于开放API的nodejs自动化翻译工具实现
1.基于开放api接口的可配置性实现
2.错误记录文件,结果记录文件,日志
3.可扩展性,目前基于百度API实现,通过同一套配置如何集成更多开放翻译API