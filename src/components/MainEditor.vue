<template>
    <div contenteditable="true" class="search-area">
        <div :key="index" v-for="(text, index) in textArray" class="single-text">
            <div class="text-area">
                {{ text }}
            </div>
            <button class="delete-button-area">
                <i class="fa-solid fa-trash"></i>
            </button>
        </div>
    </div>
    <!-- v-model can 1.react data, 2.show selected label on form -->
    <div style="display: flex">
        <el-select v-model="selectedValue" class="m-2" placeholder="select">
            <el-option label="This is __" value="This is __" />
            <el-option label="My name is __" value="My name is __" />
        </el-select>
        <el-form-item>
            <el-button @click="onSubmit" type="primary">
                決定
            </el-button>
        </el-form-item>
    </div>
</template>

<script lang="ts">
import { propsToAttrMap } from '@vue/shared';
import { defineComponent, onMounted, ref, Prop, Component } from 'vue';
import { Options, Vue } from 'vue-class-component';


const OPTIONS = [
    {
        value: 'Option1',
        label: 'Option1',
    },
    {
        value: 'Option2',
        label: 'Option2',
    },
    {
        value: 'Option3',
        label: 'Option3',
    },
]
export default class MainEditor extends Vue {
    public msg = 'hey';

    public selectedValue = '';

    public textArray = ['test', 'test2'];

    // public option1 = "option1";
    // public option2 = "option1";


    public get getMsg(): string {
        return this.msg;
    }

    created() {
        console.log("created called");
    }

    mounted() {
        console.log("mounted called");
        this.msg = 'on mounted';
    }

    public onSubmit() {
        console.log('submit');
        this.textArray.push(this.selectedValue);
    }
}
</script>

<style scoped>
.wrapper {
    color: red;
}

.search-area {
    background-color: lightblue;
    height: 35%;
    position: fixed;
    left: 0;
    bottom: 0;
    width: 100%;
}

.single-text {
    background-color: lightgreen;
    margin: 3px 0;
    display: flex;
    width: 100%;
    justify-content: center;
}

.text-area {}

.delete-button-area {
    margin: 0 20px;
}
</style>