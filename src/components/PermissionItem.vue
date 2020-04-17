<template>
    <div>
        <h1>{{this.itemData.type}}</h1>
        <label>
            <input type="checkbox" :checked="readPermission" v-model="readPermission" @change="changeCheckBox">
            <span> Read</span>
        </label>
        <br>
        <label>
            <input type="checkbox" :checked="writePermission" v-model="writePermission" @change="changeCheckBox">
            <span> Write</span>
        </label>
        <br>
        <label>
            <input type="checkbox" :checked="executePermission" v-model="executePermission" @change="changeCheckBox">
            <span> Execute</span>
        </label>
    </div>
</template>

<script>
    export default {
        name: "PermissionItem",
        data: function () {
            return {
                readPermission: this.itemData.bit[0] ==='1',
                writePermission: this.itemData.bit[1] === '1',
                executePermission: this.itemData[2] === '1'
            }
        },
        props: {
            itemData: Object
        },
        methods: {
            changeCheckBox: function () {
                let newItemBit = [~~this.readPermission, ~~this.writePermission, ~~this.executePermission].join('');
                this.$emit('changeCheckBox', newItemBit, this.itemData.id)
            }
        }
    }
</script>

<style scoped>

</style>