<section>
    <h2> Parcel vs Webpack vs Rollup </h2>
</section>
<section>
    <h4>Round 1: configuration</h4>
</section>
<section>
    <h4>Parcel</h4>
    <small>no configuration file</small>
</section>
<section>
    <h4>Webpack 4</h4>
    <pre>
        <code class="js">
'use strict'

const path = require('path'),
  webpack = require('webpack')

module.exports = {
  mode: 'production',
  entry: './reactAppSrc/index.js',
  output: {
    path: path.resolve(__dirname, '../public/built/'),
    filename: '[name].min.js',
  },
  resolve: {
    extensions: ['.js', '.jsx'],
  },
  module: {
    rules: [
      {
        test: /\.jsx$/,
        exclude: /node_modules/,
        loader: 'babel-loader'
      },
      {
        test: /\.js$/,
        exclude: /node_modules/,
        loader: 'babel-loader'
      }
    ]
  },
  plugins: []
}
        </code>
    </pre>
</section>

<section>
    <h4>Rollup</h4>
    <pre>
        <code class="js">
import babel from 'rollup-plugin-babel';

export default {
  entry: 'reactAppSrc/rollup.index.js',
  dest: 'public/built/main.min.js',
  format: 'iife',
  plugins: [
    babel({
      babelrc: false,
      exclude: 'node_modules/**',
      presets: [
        "react",

        [
          "es2015",
          {
            "modules": false
          }
        ]
      ],
      "plugins": [
        "external-helpers"
      ]
    })
  ],
};
        </code>
    </pre>
</section>

<section>
    <h4>Round 2: configuration</h4>
    <table style="font-size:60%">
    <thead>
        <tr>
            <th>Tool</th>
            <th>Build Time One</th>
            <th>Build Time Two</th>
            <th>Build Time Three</th>
            <th>Build Time Avg</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <th>Parcel</th>
            <th>14.92 s</th>
            <th>5.22 s</th>
            <th>4.36 s</th>
            <th>8.16 avg s</th>
        </tr>
        <tr>
            <th>Rollup</th>
            <th>0.570 s</th>
            <th>0.482 s</th>
            <th>0.487 s</th>
            <th>0.513 avg s</th>
        </tr>
        <tr>
            <th>Webpack</th>
            <th>3.608 s</th>
            <th>3.328 s</th>
            <th>3.844 s</th>
            <th>3.59 avg s</th>
        </tr>
    </tbody>
</table>
</section>