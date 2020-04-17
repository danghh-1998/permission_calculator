<template>
    <div>
        <div class="container">
            <PageHeader/>
            <div class="row">
                <PermissionItem :item-data="userData" @changeCheckBox="handleChangeCheckBox" class="col-3"/>
                <PermissionItem :item-data="groupData" @changeCheckBox="handleChangeCheckBox" class="col-3"/>
                <PermissionItem :item-data="otherData" @changeCheckBox="handleChangeCheckBox" class="col-3"/>
            </div>
            <hr class="my-4">
            <PermissionMonitor :monitor-data="monitorData"/>
        </div>
    </div>
</template>

<script>
    import PermissionMonitor from "@/components/PermissionMonitor";
    import PermissionItem from "@/components/PermissionItem";
    import PageHeader from "@/components/PageHeader";

    export default {
        name: "Calculator",
        components: {
            PageHeader,
            PermissionItem,
            PermissionMonitor
        },
        data: function () {
            return {
                userData: {
                    id: 0,
                    type: 'User',
                    bit: '000'
                },
                groupData: {
                    id: 1,
                    type: 'Group',
                    bit: '000'
                },
                otherData: {
                    id: 2,
                    type: 'Other',
                    bit: '000'
                }
            };
        },
        methods: {
            bitToNumber: function (bit) {
                console.log(bit);
                return (parseInt(bit[0]) * 4 + parseInt(bit[1]) * 2 + parseInt(bit[2])).toString();
            },
            bitToSymbol: function (bit) {
                let result = '';
                console.log(bit);
                result += bit[0] === '1' ? 'r' : '-';
                result += bit[1] === '1' ? 'w' : '-';
                result += bit[2] === '1' ? 'x' : '-';
                return result;
            },
            handleChangeCheckBox: function (itemBit, itemId) {
                if (itemId === 0) {
                    this.userData.bit = itemBit
                } else if (itemId === 1) {
                    this.groupData.bit = itemBit
                } else {
                    this.otherData.bit = itemBit
                }
            }
        },
        computed: {
            numericValue: function () {
                return this.bitToNumber(this.userData.bit)
                    + this.bitToNumber(this.groupData.bit)
                    + this.bitToNumber(this.otherData.bit);
            },
            symbolicValue: function () {
                return this.bitToSymbol(this.userData.bit)
                    + this.bitToSymbol(this.groupData.bit)
                    + this.bitToSymbol(this.otherData.bit);
            },
            monitorData: function () {
                return {
                    numericValue: this.numericValue,
                    symbolicValue: this.symbolicValue
                }
            }
        }
    }
</script>

<style scoped>

</style>