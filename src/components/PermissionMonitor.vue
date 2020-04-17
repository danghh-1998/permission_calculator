<template>
    <div class="row">
        <div class="col">
            <h2>Numeric value: {{monitorData.numericValue}}</h2>
        </div>
        <div class="col">
            <h2>Symbolic value: {{monitorData.symbolicValue}}</h2>
        </div>
    </div>
</template>

<script>
    export default {
        name: "PermissionMonitor",
        props: {
            monitorData: Object
        },
        data: function () {
            return {};
        }
    }
</script>

<style scoped>

</style>