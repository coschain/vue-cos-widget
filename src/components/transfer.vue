<template>
  <button @click="transfer">{{ text }}</button>
</template>

<script>
  import {apply_operation} from "../common/common";

  export default {
    name: 'Transfer',
    props: {
      text: {
        type: String,
        required: true
      },
      receiver: {
        type: String,
        required: true
      },
      amount: {
        type: String,
        require: true
      },
      memo: {
        type: String,
        require: false
      }
    },
    methods: {
      async transfer () {
        if (typeof ContentosWallet === 'undefined') {
          alert('Wallet not installed！');
          return;
        }
        try {
          let result = await apply_operation(ContentosWallet.transfer, [this.receiver, this.amount, this.memo])
          this.$emit('result', result)
        } catch (e) {
          this.$emit('error', e)
        }
      }
    }
  }
</script>

