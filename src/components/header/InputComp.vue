<template>
    <div class="m-3 d-flex align-items-center">
        <input 
        type="text" 
        class="form-control" 
        id="filterInput" 
        placeholder="Cerca"
        v-model="inputFilm"
        @keydown.enter.prevent="$emit ( 'inputResult', inputFilm)"
        >
        <button 
        type="submit" 
        class="btn btn-light ms-3"
        @click.prevent="$emit ( 'inputResult', inputFilm)"
        >Search</button>
    </div>
</template>

<script>
export default {
    name: 'InputComp',
    data() {
        return{
            inputFilm: '',
        }
    }
}
</script>

<style lang="scss" scoped>

</style>