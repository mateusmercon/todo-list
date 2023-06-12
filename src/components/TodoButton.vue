<script setup>

</script>

<template>
    <div>
        <button>
            <slot>Create</slot>
        </button>
    </div>
</template>


<style lang="scss" scoped>
button {
    color: #223461;
    padding: 8px 16px;
    border: none;
}
</style>