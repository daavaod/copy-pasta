<template>
    <div class="cp-container">
        <ul>
            <CpItem v-for="item in cpDataLocal" :key="item.id" :itemData="item" @emitInput="handleEmitInput" @emitDelete="handleEmitDelete" @emitChange="handleEmitChange"/>
        </ul>
        <div class="cp-text-wrap" v-if="cpDataLocal.length > 0">
            Text in clipboard: <strong>{{ copiedText }}</strong>
        </div>
        <div class="btn-wrap">
            <button @click.prevent="toggleDialog" class="primary">Add item</button>
        </div>
        <CpGenerate :activate="activateDialog">
            <template v-slot:input>
                <ul class="dialog-actions">
                    <li><input type="text" v-model="inputTitle"></li>
                    <li><button @click="handleCreate" class="primary width">Create</button></li>
                    <li><button @click="toggleDialog" class="normal width">Close</button></li>
                </ul>
            </template>
        </CpGenerate>
    </div>
</template>

<script>
import cpData from '../../scripts/cp-data.js'
import CpItem from './CpItem.vue'
import CpGenerate from './CpGenerate.vue'

export default {
    name: "CpContainer",
    components: {
        CpItem,
        CpGenerate
    },
    props: {

    },
    data() {
        return {
            copiedText: '',
            cpDataLocal: null,
            activateDialog: false,
            inputTitle: ''
        }
    },
    computed: {
        
    },
    methods: {
        toggleDialog() {
            this.activateDialog = !this.activateDialog;
            this.inputTitle = ''
        },
        handleEmitInput(val) {
            this.copiedText = val;
        },
        handleEmitDelete(val) {
            let getLS = JSON.parse(localStorage.getItem('cpData'));

            let removeItem = getLS.filter(item => {
                return item.id !== val
            })

            localStorage.setItem('cpData', JSON.stringify(removeItem))

            this.getCpLocalStorage();

        },
        handleEmitChange(val) {
            this.handleUpdate(val.id, val.text);
        },
        generateId() {
            return Math.floor(Math.random() * 10000);
        },
        handleUpdate(id, text, title) {
            let getLS = JSON.parse(localStorage.getItem('cpData'));

            let updateItem = getLS.map(item => {
                if(item.id === id) {
                    let newItem = {
                        id: item.id,
                        text: text,
                        title: title
                    }
                    return newItem
                } else {
                    return item
                }
            })

            localStorage.setItem('cpData', JSON.stringify(updateItem))

            this.getCpLocalStorage();
        },
        handleCreate() {
            let generateId = this.generateId();
            let getLS = JSON.parse(localStorage.getItem('cpData'));

            let payload = {
                id: generateId,
                text: '',
                title: this.inputTitle
            }

            getLS.push(payload);

            localStorage.setItem('cpData', JSON.stringify(getLS))

            this.getCpLocalStorage();
            this.toggleDialog();
        },
        setLocalStorage(value) {
            let getCurrent = this.getCpLocalStorage();

            localStorage.setItem('cpData', JSON.stringify())
        },
        getCpLocalStorage() {
            let cpDataLocal = localStorage.getItem('cpData');

            if(cpDataLocal) {
                this.cpDataLocal = JSON.parse(cpDataLocal);
            } else {

                let payload = [{
                    id: this.generateId(),
                    text: '',
                    title: ''
                }]

                localStorage.setItem('cpData', JSON.stringify(payload))
            }
        }
    },
    created() {
        this.getCpLocalStorage();
    }
};
</script>

<style>
    .cp-container {
        padding: 20px;
        max-width: 1024px;
        margin: 0 auto;
    }
    .cp-container ul {
        width: 100%;
    }
    .cp-container li {
        display: flex;
        gap: 20px;
        margin-bottom: 20px;
        align-items: center;
        padding-top: 20px;
    }
    .cp-container li button {
        flex: 0 0 auto;
    }
    .cp-container li div {
        flex: 1 1 auto;
        position: relative;
    }
    .cp-container li div label {
       display: block;
       position: absolute;
       top: 10px;
       left: 10px;
       font-style: italic;
       font-size: 12px;
       color: #cccccc;
    }
    .cp-container li div textarea {
       width: 100%;
       padding-top: 30px;
    }
    .btn-wrap {
        text-align: center;
    }
    .cp-text-wrap {
        padding: 20px;
    }
    .cp-text-wrap strong {
        font-size: 16px;
    }
    .dialog-actions li {
        margin-bottom: 0;
    }
</style>