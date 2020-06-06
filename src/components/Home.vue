<template>
    <el-container>
        <Main></Main>
    </el-container>
</template>
<script>
import Main from 'components/layout/Main'
export default {
    components: {
        Menu,
        Main
    }
}
</script>
<style>
.el-container {
    height: 100%;
}
</style>