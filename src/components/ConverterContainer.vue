<script>
    import OptionsSelect from '../components/OptionsSelect.vue'

    export default {
        components: {
            OptionsSelect,
        }
    }
</script>

<template>
    <h1>Currency Convert</h1>
    <div class="row">
        <div class="col-6">
            <select name="firstCurr" id="firstCurr">
                <OptionsSelect></OptionsSelect>
            </select>
        </div>
    
        <div class="col-6">
            <select name="secondCurr" id="secondCurr">
                <OptionsSelect></OptionsSelect>
            </select>
        </div>
    </div>
</template>

<script>
</script>