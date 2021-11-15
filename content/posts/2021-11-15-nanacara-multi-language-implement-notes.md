---
title: "Nanacara multi-language implement notes"
slug:
description: ""
date: 2021-11-15 11:00:41
author: ThaiLe
tags:
cover:
fullscreen: false
---
## Packages:
- `react-i18next`
- `react-native-localize`

## Organizing translations:
### Folder structure

```javascript
 |-localization
 | |-vi
 | | |-setting.js
 | | |-auth.js
 | | |-index.js
 | | |-common.js
 | |-ja
 | | |-setting.js
 | | |-auth.js
 | | |-index.js
 | | |-common.js
 | |-languageDetectorPlugin.js
 | |-i18n.js
```

`ja(vi)/common.js` -> language file for common text

`ja(vi)/auth.js` -> language file for auth module

`ja(vi)/setting.js` -> language file for setting module

`ja(vi)/....js` -> other modules

> So each module will have one file - one namespace

## How to use translation functions

Use `useTranslation` hook in function components

```javascript
import React from 'react'
import { useTranslation } from 'react-i18next'
export function LoginForm() {
  // auth is namespace you want to load
  const { t, i18n } = useTranslation('auth')
  // or const [t, i18n] = useTranslation('auth')
  return <Text>{t('login_title')}</Text>
}
```

Use `withTranslation` HOC in class/function components

```javascript
import React from 'react'
import { withTranslation } from 'react-i18next'
class LoginForm extends React.Component {
  render() {
    const { t } = this.props
      return <Text>{t('login_title')}</Text>
  }
}
export default withTranslation('auth')(LoginForm)
```

> For load text from other namespace, just use `t('namespace:key')`. Example: `t('common:okLabel')`

### Change language

```javascript
  const { t, i18n } = useTranslation()

  function onChangeLanguage(lngCode) {
    i18n.changeLanguage(lngCode)
  }
```

This function will trigger rerender app, also update current language on redux

### Notes
- Get current language from i18n: `i18n.language`
- Get current language from redux: `store -> app.language`
- Redux value will sync with i18n, please check code in file `languageDetectorPlugin.js`

## More documents:
- https://www.i18next.com/
- https://react.i18next.com/


