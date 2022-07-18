<template>
    <div class="search-area">
        <div :key="index" v-for="(textObject, index) in textObjectArray" class="text-area">
            <p class="single-text" contenteditable="true" aria-multiline="true"
                style="white-space: pre-wrap; min-width: 1px;">
                {{ textObject.text }}
            </p>
            <el-button @click="onDeleteText(textObject.id)" class="delete-button-area" round>
                <i class="fa-solid fa-trash"></i>
            </el-button>
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
import { ThumbInstance } from 'element-plus';
import { defineComponent, onMounted, ref, Prop, Component } from 'vue';
import { Options, Vue } from 'vue-class-component';
import { v4 as uuidv4 } from 'uuid';
import { Console } from 'console';


export default class MainEditor extends Vue {
    public msg = 'hey';

    public selectedValue = '';

    public textArray: { id: number, text: string }[] = [
        { id: 1, text: 'initial text' },
    ];
    // public textObjectArray: {[key: string]: string} = {};
    public textObjectArray: { id: string, text: string }[] = [
    ];

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

        const out = document.querySelector('.search-area')!;
        out.addEventListener(
            'keydown', (e) => {
                const target = e as KeyboardEvent;
                if (target.code === 'Enter') {
                    // TODO: Add next line when Enter pressed
                    console.log('return');
                }
            }
        );
        // out.addEventListener('input', () => {
        //     if (out.innerHTML === '') {
        //         out.innerHTML = '<p>test</p>';
        //     }
        // //     out.textContent = out.innerHTML;
        // });
    }

    public onSubmit() {
        const uuid = uuidv4();
        const obj = { id: uuid, text: this.selectedValue };
        // this.textObjectArray[uuid] = this.selectedValue;
        this.textObjectArray.push(obj);
        for (const textObject of this.textObjectArray) {
            console.log(textObject.id);
            console.log(textObject.text);
        }
    }

    public onDeleteText(index: string) {
        // const indexOfObject = this.textObjectArray.findIndex((element) => element.id === index);
        const indexOfObject = this.textObjectArray.findIndex(element => element.id === index);
        console.log(indexOfObject);
        this.textObjectArray.splice(indexOfObject, 1);
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

.text-area {
    background-color: lightgreen;
    margin: 3px 0;
    display: flex;
    width: 100%;
    justify-content: center;
    align-items: center;
}

.single-text {
    width: 100%;
    margin: 0 5rem;
    text-align: start;
}

.delete-button-area {
    margin: 0 20px;
    height: 20px;
}
</style>