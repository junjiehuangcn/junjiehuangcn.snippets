```js
$(window).bind('beforeunload', () => localStorage.removeItem('TOKEN'))

export default {
  get() {
    let localToken = localStorage.getItem('TOKEN')
    let sessionToken = sessionStorage.getItem('TOKEN')
    // 新开窗口
    if (localToken && !sessionToken) {
      sessionStorage.setItem('TOKEN', localToken)
      return localToken
    }
    // 刷新页面
    if (!localToken && sessionToken) {
      localStorage.setItem('TOKEN', sessionToken)
      return sessionToken
    }
    // 切换用户
    if (localToken && localToken !== sessionToken) {
      sessionStorage.setItem('TOKEN', localToken)
      return location.reload(true)
    }
    return localToken
  },
  set(token) {
    if (token === undefined || token === null) { return }
    localStorage.setItem('TOKEN', token)
    sessionStorage.setItem('TOKEN', token)
  },
  clean() {
    localStorage.removeItem('TOKEN')
    sessionStorage.removeItem('TOKEN')
  }
}

```
2
