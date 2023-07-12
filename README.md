# Getting started

```shell
yarn install
npx pod-install
yarn ios # or yarn android
```

# How to patch the library

1. open `node_modules/@sendbird/uikit-utils/src/sendbird/message.ts`
2. edit `function shouldRenderReaction` like below
```ts
export function shouldRenderReaction(channel: SendbirdBaseChannel, reactionEnabled: boolean) {
   if (channel.isOpenChannel()) {
      return false;
   }

   if (channel.isGroupChannel()) {
      if (channel.isBroadcast) return false;
      // if (channel.isSuper) return false;
      if (channel.isEphemeral) return false;
   }

   return reactionEnabled;
}
```
3. [patch package](https://github.com/ds300/patch-package)
```shell
npx patch-package @sendbird/uikit-utils
```
