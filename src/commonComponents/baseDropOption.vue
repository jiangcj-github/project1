<template>
    <div class="dropItem">
        <slot></slot>
    </div>
</template>

<script>

export default {
    name: "baseDropOption",
}
</script>

<style lang="scss" scoped>
.dropItem {  
    width: 100px;
    text-align: center;
    line-height: 30px;
    font-size: 13px;
    color: #888;
    margin: 2px 0;
    cursor: pointer;
    transition: all 0.3s;
    &:hover {
        background: #F9F9FC;
        color: #4780F7;
    }
}
</style>
