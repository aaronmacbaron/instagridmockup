<template>
    <div :class="'image-block '+classname">
        <input v-if="!fileSelected" type="file" :id="id"  @change="getFilename" />
        <div v-if="fileSelected" @dblclick="unsetFilename" @click="setSwitchCandidate" :style="(filename) ? 'background:url('+filename+')' : ''" class="grid-image"></div>
    </div>
</template>
<script>
export default {
    name : 'grid-item',
    props: ['id','classname'],
    methods : {
        getFilename : function(e){
            this.fileSelected = true;
            let fileInput = document.getElementById(this.id);
            this.filename = URL.createObjectURL(e.target.files[0]);
        },
        unsetFilename : function(){
            this.filename = '';
            this.fileSelected = false;
        },
        setSwitchCandidate : function(){
            let current_filename = this.filename;
            if(this.$parent.switchingObject !== null){
                this.filename = this.$parent.switchingObject.filename;
                this.$parent.switchingObject.filename = current_filename;
                this.$parent.switchingObject = null;
            }else{  
                this.$parent.switchingObject = this;
            }
            
        }
    },
    data : function() {
        return {
            fileSelected : false,
            filename : ''
        }
    },
    mounted : function(){

    }
}
</script>
<style scoped>
    .remove-image{
        position:relative;
        color:#fff;
        background:crimson;
        padding:3px 8px;
        text-decoration:none;
        border-radius:3px;
        display:none;
        max-width:100px;
        margin-top:-45px;
        left:-20px;
        float:right;
    }
    .btn-switch-candidate{
        position:relative;
        color:#fff;
        background:skyblue;
        padding:3px 8px;
        text-decoration:none;
        border-radius:3px;
        display:none;
        max-width:100px;
        margin-top:-45px;
        left:20px;
        float:left;
    }
    .grid-image{
        width:100%;
        height:30vw;
        position:relative;
        display:block;
        background-size: cover !important;
        background-position: center center !important;
    }
    .image-block:hover .remove-image{
        display:block;
    }
    .image-block:hover .btn-switch-candidate{
        display:block;
    }
</style>
