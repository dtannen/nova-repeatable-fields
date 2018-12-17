<template>
    <div>
        <select
            :id="subField.name"
            :name="subField.name"
            class="w-full form-control form-select"
            :value="value"
            @change="onChange($event.target.value)">
            <option
                value=""
                v-text="placeholder"
                selected
                disabled
            ></option>
            <option
                v-for="(label, name) in subField.options"
                :value="name"
                :selected="name == value"
                v-text="label"
            ></option>
        </select>
    </div>

</template>

<script>

    export default {

        props: [
            'subField',
            'value',
            'index'
        ],

        computed:{
            placeholder(){
                return (this.subField.placeholder === this.subField.label)
                    ? 'Choose an option'
                    : this.subField.placeholder
            }
        },

        mounted() {
            if (this.value == 'Other') {
                if (document.getElementsByClassName('h-sub-field').length > 0) {
                    document.getElementsByClassName('h-sub-field')[this.index].className = document.getElementById('other').className.replace(/\bhidden\b/g, '')
                }
            }
        },

        methods:{
            onChange(value) {
                if (value == 'Other') {
                    if (document.getElementsByClassName('h-sub-field').length > 0) {
                        document.getElementsByClassName('h-sub-field')[this.index].className = document.getElementById('other').className.replace(/\bhidden\b/g, '')
                    }
                } else {
                    if (document.getElementsByClassName('h-sub-field').length > 0 && 'Other' in this.subField.options) {
                        document.getElementsByClassName('h-sub-field')[this.index].className = 'hidden h-sub-field w-full form-control form-input form-input-bordered'
                        document.getElementsByClassName('h-sub-field')[this.index].value = ''
                    }
                }
                this.$emit('input', value)
            }
        }

    }
</script>
