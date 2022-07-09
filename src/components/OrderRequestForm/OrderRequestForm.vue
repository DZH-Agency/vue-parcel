<template>
  <el-form :model="form" label-width="auto" label-position="top">
    <el-form-item label="City - From">
      <el-select
        :model-value="form.cityFrom"
        filterable
        placeholder="Select city"
        @change="updateField('cityFrom', $event)"
      >
        <el-option
          v-for="city in cityChoices"
          :key="city.id"
          :label="city.name"
          :value="city.name"
        />
      </el-select>
    </el-form-item>
    
    <el-form-item label="City - To">
      <el-select
        :model-value="form.cityTo"
        filterable
        placeholder="Select city"
        @change="updateField('cityTo', $event)"
      >
        <el-option
          v-for="city in cityChoices"
          :key="city.id"
          :label="city.name"
          :value="city.name"
        />
      </el-select>
    </el-form-item>
    
    <el-form-item label="Parcel type">
      <el-select
        :model-value="form.parcelType"
        filterable
        placeholder="Select parcel type"
        @change="updateField('parcelType', $event)"
      >
        <el-option
          v-for="type in parcelTypeChoices"
          :key="type.id"
          :label="type.name"
          :value="type.name"
        />
      </el-select>
    </el-form-item>
    
    <el-form-item label="Date of dispatch">
      <el-date-picker
        v-model="dateOfDispatch"
        type="date"
        placeholder="Pick a date"
      />
    </el-form-item>
    
    <el-form-item label="Parcel description">
      <el-input
        :model-value="form.parcelDescription"
        type="textarea"
        placeholder="Enter parcel description"
        @input="updateField('parcelDescription', $event)"
      />
    </el-form-item>
    
    <el-form-item>
      <el-button type="primary" @click="$emit('save')">
        Save
      </el-button>
      
      <el-button type="info" @click="$emit('cancel')">
        Cancel
      </el-button>
    </el-form-item>
  </el-form>
</template>

<script setup>
import { computed, ref } from 'vue'

const props = defineProps({
  form: {
    type: Object,
    required: true
  }
})

const emit = defineEmits({
  'update-field': payload => 'fieldName' in payload && 'fieldValue' in payload,
  'save': null,
  'cancel': null
})

function updateField(fieldName, fieldValue) {
  emit('update-field', {fieldName, fieldValue})
}

// Temporary solution for el-date-picker due to issue
// Issue link - https://github.com/element-plus/element-plus/issues/8523
const dateOfDispatch = computed({
  get() {
    return props.form.dateOfDispatch
  },
  set(newValue) {
    updateField('dateOfDispatch', newValue)
  }
})

const cityChoices = ref([
  {
    name: 'Kharkiv',
    id: '1'
  },
  {
    name: 'Lviv',
    id: '2'
  },
  {
    name: 'Kyiv',
    id: '3'
  },
])

const parcelTypeChoices = ref([
  {
    name: 'Gadgets',
    id: '1'
  },
  {
    name: 'Drinks',
    id: '2'
  },
  {
    name: 'Clothes',
    id: '3'
  },
  {
    name: 'Medicines',
    id: '4'
  },
  {
    name: 'Other',
    id: '5'
  },
])

</script>

<style scoped>

</style>