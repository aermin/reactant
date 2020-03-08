# reactant

![Node CI](https://github.com/unadlib/reactant/workflows/Node%20CI/badge.svg)

A framework for building React web applications, inspired by [Angular](https://angular.io/).

### Example

```tsx
import React from 'react';
import {
  ViewModule,
  createApp,
  injectable,
  inject,
  optional,
  useConnector,
  defaultProps,
  action,
  createSelector,
} from 'reactant';
import { render } from 'reactant-web';

@injectable()
class Foo {
  text = 'foo';
}

@injectable()
class Count {
  state = {
    num: 0,
  };

  @action
  increase() {
    this.state.num += 1;
  }
}

@injectable()
class DashboardView extends ViewModule {
  constructor(public count: Count) {
    super();
  }

  getSum = createSelector(
    () => this.count.state.num,
    num => num + 1
  );

  getData = () => ({
    num: this.getSum(),
  });

  component() {
    const data = useConnector(this.getData);
    return (
      <div onClick={() => this.count.increase()} id="increase">
        {data.num}
      </div>
    );
  }
}

@injectable()
class HomeView extends ViewModule {
  text = 'app';

  getProps(version: string) {
    return {
      version: `${this.text} v${version}`,
    };
  }

  @defaultProps({
    version: '0.0.1',
  })
  component(props: { version?: string }) {
    const data = useConnector(() => this.getProps(props.version!));
    return <span id="version">{data.version}</span>;
  }
}

@injectable()
class AppView extends ViewModule {
  constructor(
    @optional() public foo: Foo,
    @inject('homeView') public homeView: InstanceType<typeof HomeView>,
    public dashboardView: DashboardView
  ) {
    super();
  }

  component() {
    return (
      <>
        <div id="foo">{this.foo.text}</div>
        <this.homeView.component version="0.1.0" />
        <this.dashboardView.component />
      </>
    );
  }
}

const app = createApp({
  modules: [Foo, { provide: 'homeView', useClass: HomeView }],
  main: AppView,
  render,
});
```

## Goal

- Immutable
- Easy
- High-performance
- Flexible

## Libraries

- react
- redux
- react-router
- inversify
- immer
- reselect

## Tips

- `ViewModule` class `component` support inheritance, and it does not support call `super.component` for JSX Element but support call function.
- `@action` support inheritance and call `super`.
- Performance optimization
  - Selector from `createSelector`can be passed in immutable state.
  - `batch` can be used to optimize rendering performance.
  - `dispatch` and `createState` support prue Redux action and reducer.
- Decorators
  - Default injection, no require `@inject` unless binding token.
  - All decorators support any token.
  - `@multiInject` and `@multiOptional` require token parameter.

## API

### reactant

- ViewModule
- createApp
- useConnector
- @injectable
- @action
- @optional
- @inject
- @multiInject
- @multiOptional
- @module
- createSelector
- @defautlProps
- dispatch
- createState
- batch

## TODO

- [x] selector
- [x] action
- [x] multiple ViewModule instances
- [x] optimize action
- [x] @defautlProps
- [x] useConnector
- [x] check `batch`
- [x] Enhance DI
  - [x] optional
  - [x] inject
  - [x] multi-inject
  - [x] multi-optional
- [x] @module
- [x] middleware
- [x] pluggable
- [x] storage
- [x] router

- [ ] tracker
- [ ] hierarchical DI systems
- [ ] mobx
- [ ] Form
- [ ] Network
- [ ] i18n
- [ ] Accessibility
- [ ] C4
- [ ] Micro Front-end
- [ ] CLI
- [ ] VSCode Plug-in
- [ ] testing
- [ ] SSR
- [ ] Hook
- [ ] Support JavaScript
- [ ] Plug-in system
