# Vue Play

Play and demonstrate your Vue components, inspired by [react-storybook](https://github.com/kadirahq/react-storybook).

## Play it in seconds

The only thing you need to install is `vue-play-cli`:

```bash
$ npm install -g vue-play-cli
```

Then, let's play with your Button component, create a `play.js` in the root directory of your project (anywhere else is ok):

```jsx
// you don't need to install vue-play!
import {play} from 'vue-play'
// import the button you wanna play
import MyButton from './components/MyButton.vue'

play({
  Button: {
    'with text'(h) {
      return <MyButton>Hello Play!</MyButton>
    },
    'with rounded border'(h) {
      return <MyButton rounded={true}>I'm rouned!</MyButton>
    }
  }
})
```

Run the play script with command `vue-play`, and [see it in action!](http://vue-play-button.surge.sh) ([code](https://github.com/egoist/vue-play-button))

```bash
$ ~/my-button-component vue-play
> play at http://localhost:5000
```

## Advanced

### States and methods

How do I write play script so that my component can call a method or update a state? Well, you can simply:

```js
// pass a component object
play({
  Button: {
    'with text': {
      data() {
        return {/* ... */}
      },
      methods: {
        handleClick() {/* ... */}
      },
      render(h) {
        return <MyButton on-click={this.handleClick}>text</MyButton>
      }
    }
  }
})
```

## Customize webpack config

Check out the [default webpack config](https://github.com/egoist/vue-play/blob/master/packages/vue-play-cli/lib/make-config.js), in brief, you can play with:

**babel**: es2015 stage-2<br>
**postcss**: postcss-nested postcsss-simple-vars<br>
**image and fonts**: file-loader

### The simple? way

Provide your own webpack.config.js and pass the path to it in `--config` option. In this way you will need to install loaders and plugins you used in your project.

### The hard? way

Provide a config file which exports a function, taking `config` and `options` as arguments. And you can modify the config as you like, and finally pass the path to it in `--config` option.

```js
// update-config.js
// config - webpack config
// options - cli arguments
module.exports = (config, options) {
  config.postcss.push(require('postcss-mixins'))
  return config
}
```

## License

[MIT](https://egoist.mit-license.org) &copy; [EGOIST](https://github.com/egoist)
