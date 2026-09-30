[Nuxt MDC](https://github.com/nuxt-content/mdc/blob/main/README.md)

This primarily addresses the issue where excessive content in the code field during a highlight GET request causes a 431 error.

```ts
const long = (code || '').split('\n').length > 260

  const result = await $fetch<HighlightResult | undefined>('/api/_mdc/highlight', {
    method: long ? 'POST' : 'GET',
    [long ? 'body' : 'params']: {
      code,
      lang,
      theme: JSON.stringify(theme),
      options: JSON.stringify(options),
    },
  })
```

```ts
const { code, lang, theme: themeString, options: optionsStr } = event.method === 'POST' ? await readBody(event) : getQuery(event)
```