<template>
    <div>
        <p v-show="isVisible" style="cursor: pointer;">{{ value }}</p>
        <input type="text" placeholder="Введите текст" v-show="!isVisible" v-model="internalValue" @change="inputChange">
    </div>
</template>

<script>
export default {
    props: {
        value: {
            type: String,
            required: true
        },
        isVisible: {
            type: Boolean,
            required: true
        }
    },
    data() {
        return {
            internalValue: this.value,
        };
    },
    methods: {
        inputChange() {
                this.$emit('update:value', this.internalValue);
        }
    }
}
</script>
