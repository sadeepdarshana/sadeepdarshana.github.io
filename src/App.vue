<template>
    <div id="app">


        <NormalSite v-if="file==null"></NormalSite>
        <WNViewer :contentName="file" v-if="file!=null"></WNViewer>



    </div>
</template>

<script>
    import DirectoryStructure from './components/DirectoryStructure.vue'
    import QRPage from './components/QRPage.vue'
    import ThePage from "./components/ThePage";
    import WNViewer from "./components/WNViewer";
    import VueRouter from 'vue-router'
    import NormalSite from './NormalSite'

export default {
    name: 'app',
    components: {
        NormalSite:NormalSite,
        ThePage:ThePage,
        WNViewer:WNViewer,
        DirectoryStructure: DirectoryStructure,
        QRPage: QRPage,
        VueRouter:VueRouter
    }
    ,
    methods:{
        setUser(uid){
            this.$cookie.set('uid', uid, { expires: '1Y' });
            this.refresh();
        },
        clearUser(){
            this.$cookie.set('uid', "no", { expires: '1Y' });
            this.refresh();
        },
        refresh(){
            this.userLoaded = this.$cookie.get('uid') != null && this.$cookie.get('uid') !== "no";
        }
    },
    created(){
        this.refresh();

    },
    data() {
        return {
            userLoaded:false,
            file:this.$router.currentRoute.query.file
        }
    }
}
</script>

<style>
#app {
    font-family: 'M PLUS 1p', sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    color: #2c3e50;




    -moz-user-select: -moz-none;
    -khtml-user-select: none;
    -webkit-user-select: none;

    /*
      Introduced in IE 10.
      See http://ie.microsoft.com/testdrive/HTML5/msUserSelect/
    */
    -ms-user-select: none;
    user-select: none;
}


</style>
