<script setup>
</script>
<template>
    <button>
        <!-- here Create is a fallback value what ever we wrap inside the component inside parent component will be displayed inside slot -->
        <slot>
            Create
        </slot>
    </button>
</template>
<style lang="scss" scoped>
button {
    padding: 8px 16px;
    border: none;
}
</style>