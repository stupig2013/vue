# Vue source code reading notes

## 1.Entry
- Vue (core/instance/index.js) 
- Vue.prototype._init (core/instance/init.js)
- Vue.prototype.$mount (platforms/web/entry-runtime-with-compiler.js)
  - compileToFunctions (platforms/web/compiler/index.js)
    > generate compile function `render`
- Vue.prototype.$mount (platforms/web/runtime/index.js)
- mountComponent (core/instance/lifecycle.js)

  ```
    updateComponent = () => {
      vm._update(vm._render(), hydrating)
    }

    new Watcher(vm, updateComponent, noop, {
      before () {
        if (vm._isMounted && !vm._isDestroyed) {
          callHook(vm, 'beforeUpdate')
        }
      }
    }, true /* isRenderWatcher */)
  ```
- Vue.prototype._render (core/instance/render.js)
  
  ```
    vnode = render.call(vm._renderProxy, vm.$createElement)
  ```
  > _renderProxy = `vm`
- Vue.prototype._update (core/instance/lifecycle.js)
- createPatchFunction (core/vdom/patch.js)
