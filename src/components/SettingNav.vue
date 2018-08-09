<template>
    <div :style="{width:width}" class="nav-side">
        <a href="#" class="nav-item">基础设置</a>
        <a href="#" class="nav-item">我的收藏</a>
        <a href="#" class="nav-item">我的发布</a>
        <a href="#" class="nav-item">浏览足迹</a>
    </div>
</template>

<script>
    import "../css/sidenav.css";
    export default {
       props:{
            width:[ 'width' ],
       } 
    }
</script>

<style scoped>
    

</style>
