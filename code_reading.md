# Vue source code reading notes

## 1.Entry (mount)
1. Vue (core/instance/index.js) 
2. Vue.prototype._init (core/instance/init.js)
3. Vue.prototype.$mount (platforms/web/entry-runtime-with-compiler.js)
    - compileToFunctions (platforms/web/compiler/index.js)
      > generate compile function `render`
4. Vue.prototype.$mount (platforms/web/runtime/index.js)
5. mountComponent (core/instance/lifecycle.js)

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
6. Watcher.prototype.get (core/observer/watcher.js)

    ```
        value = this.getter.call(vm, vm)
    ```  
7. Vue.prototype._render (core/instance/render.js)
  
    ```
      vnode = render.call(vm._renderProxy, vm.$createElement)
    ```
    > _renderProxy = `vm`
8. Vue.prototype._update (core/instance/lifecycle.js)
9. patch (core/vdom/patch.js)
10. createElm (core/vdom/patch.js)

    ```
        if (createComponent(vnode, insertedVnodeQueue, parentElm, refElm)) {
          return
        }
        ...
        insert(parentElm, vnode.elm, refElm)
    ```
11. createComponent (core/vdom/patch.js)
12. componentVNodeHooks.init (core/vdom/create-component.js)
13. createComponentInstanceForVnode (core/vdom/create-component.js)

    ```
      return new vnode.componentOptions.Ctor(options)
    ```
    > Ctor come from:
    - _createElement (core/vdom/create-element.js)

      ```
        Ctor = resolveAsset(context.$options, 'components', tag)
      ```
    - initAssetRegisters (core/global-api/assets.js)

      ```
        definition = this.options._base.extend(definition)
      ```
    - Vue.extend (core/global-api/extend.js)

      ```
        const Sub = function VueComponent (options) {
          this._init(options)
        }
      ```
14. Vue.prototype.$mount (platforms/web/entry-runtime-with-compiler.js)
    > cycle from step 3
    ```
      child.$mount(hydrating ? vnode.elm : undefined, hydrating)
    ```


## 2.update

