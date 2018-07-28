### I. Setting
---
- Trong quá trình cài đặt dù đã chạy hết các câu lệnh yêu cầu nhưng source vẫn ko chạy được. Dưới đây là các câu lênh cần chạy thêm:

```javascript
npm install --save-dev webpack
npm install --save-dev cross-env
npm install "cross-env"
npm install -g win-node-env
```

- Trong file ```package.json``` nên thêm dòng này: 
```javascript
"scripts": {
  "build": "cross-env NODE_ENV=production webpack --config build/webpack.config.js"
}
```

### II. App: React Universal Blog
---
**Reference:**

- https://www.sitepoint.com/building-a-react-universal-blog-app-a-step-by-step-guide/
- https://github.com/sitepoint-editors/react-universal-blog

**Getting Started**

1. Node.js for package management and server-side rendering
2. React for UI views
3. Express for an easy back-end JS server framework
4. React Router for routing
5. React Hot Loader for hot loading in development
6. Flux for data flow
7. Cosmic JS for content management

### III. App: React Universal Blog
---
**1.**

```javascript

```

### IV. App: React Universal Blog
---
**1.**

```javascript

```

### V. App: React Universal Blog
---
**1.**

```javascript

```


