<template>
    <div>
        <div class="operations">
            <div class="small float-left">
                <label class="btn btn-secondary mr-2 btn-sm pl-3 pr-3 mb-0">
                    Upload <input type="file" @change="processFile($event)" onclick="this.value = null" hidden>
                </label><br />
                <small>An Excel Spreadsheet maintained to upload student marks</small>
            </div>
        </div>
    </div>
</template>

<script>
import { useStore } from "vuex";
import store from "../store";
export default {
    setup: () => { },
    data() {
        return {
            store: useStore(),
            user: store.getters.getCurrentUser,
            marksFile: null,
            data: null,
        };
    },
    methods: {
        processFile: async function (e) {
            this.marksFile = e.target.files[0];
            if (this.marksFile.name.toLowerCase().split('.')[this.marksFile.name.toLowerCase().split('.').length - 1] == 'xlsx') {
                if (typeof (FileReader) != "undefined") {
                    const result = await new Promise(resolve => {
                        var reader = new FileReader();
                        reader.addEventListener('load', () => resolve(reader.result), false);
                        reader.readAsArrayBuffer(this.marksFile);
                    });
                    this.data = new Uint8Array(result);
                    const response = await axios.post('/.netlify/functions/marks/process', { content: this.data });
                    console.log(response.data);
                } else {
                    alert("This browser does not support HTML5.");
                }
            } else {
                alert("Please upload a valid Excel file.");
            }
        }
    }
};
</script>