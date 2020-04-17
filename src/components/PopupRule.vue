<template>
    <div class="wrapper-popup " v-bind:class="getClassPopup">
        <div class="rule">
            <h3>Luat choi</h3>
            <p>Luat choiLuat choiLuat choiLuat choiLuat choiLuat choi</p>
            <button class="confirm" v-on:click="confirm">Da hieu </button>
        </div>
    </div>
</template>
<script>
export default {
    name:"popup-rule",
    props:{
        isOpenPopup : {type:Boolean,default:false}
    },
    data() {
        return {
            
        }
    },
    methods: {
        confirm(){
            this.$emit('handleConfirm');
        }
    },
    computed: {
        getClassPopup(){
            return { 'open-popup':this.isOpenPopup }
        }
    },
}
</script>
<style lang="">
    .wrapper-popup {
        position:fixed;
        top : 0;
        left:0;
        bottom:0;
        right:0;
        background-color:rgba(0,0,0,0.4);
        opacity: 0;
        visibility:hidden;
         transition:all .3s ease
    }

    .wrapper-popup.open-popup {
        opacity: 1;
        visibility:visible
    }

    .rule{
        position:absolute;
        width:300px;
        padding:20px;
        top:40%;
        left:40%;
        background-color:#fff;
        transition:translate(-50%,-50%) scale(1.2);
        font-family:Arial;
         transition:all .3s ease
    }
    .open-popup .rule {

        transition:translate(-50%,-50%) scale(1);
    }
    .rule .confirm{
        margin-top:20px;
        padding:8px 15px;
        border:2px solid #333;
        background-color:#fff;
        transition:all .3s ease
    }
    .rule .confirm:hover{
       color:#fff;
        background-color:#333
    }
</style>