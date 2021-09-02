## dev mode

```sh
npm run dev
```

## build

```sh
npm run build
```

/docs/.vuepress/dist is the folder we want to deploy  
netlify will auto-deploy when pushing to github after npm run build
so npm run build, then git push origin master

## config

/docs/.vuepress/config.js
change sidebar(folder url) settings in themeConfig
vuepress will make md title as sidebar title
