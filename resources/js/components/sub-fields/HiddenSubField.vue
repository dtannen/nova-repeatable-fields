<template>
    <div>
        <input
            :id="subField.name"
            :name="subField.name"
            type="text"
            class="hidden h-sub-field w-full form-control form-input form-input-bordered"
            :value="value"
            :placeholder="subField.placeholder"
            @input="$emit('input', $event.target.value)"
            @change="$emit('input', $event.target.value)"
        />
    </div>

</template>

<script>

    export default {

        props: [
            'subField',
            'value'
        ],

    }
</script>
