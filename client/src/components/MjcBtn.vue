<!-- 커스텀할 수 있는 버튼을 컴포넌트로 만듦 -->
<template>
  <div 
    class="mjc-btn" 
        :style="{ 
            background: background || '#eee', 
            color:fontcolor || '#000' 
        }"
        @click="btnClick"
    >
    <slot></slot>
  </div>
</template>

<script>
export default {
    props:["label", "background", "fontcolor"],
    mounted() {
        console.log(this.label);
    },
    methods: {
        btnClick(){
           this.$emit("changeBackground", "#ffff00");
           this.$emit("click", this.background);
        },
    },
};
</script>

<style scoped>
.mjc-btn{
    padding:5px 10px;
    background: #eee;
    border-radius:10px;
    font-size:16px;
    text-align: center;
    cursor: pointer;
}

</style>