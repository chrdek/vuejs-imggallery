<template>
<span id="dropdown__el">
<label>Viewing {{configSelected}} items / page</label>
<select class="sel--main-blue" v-on:change="(e) => this.$emit('LimitChange',e)" v-model="configSelected">
	<option value="10">10</option>
	<option value="20">20</option>
	<option value="30">30</option>
	<option value="50">50</option>
	<option value="80">80</option>
	<option value="90">90</option>
	<option value="100">100</option>
</select>
</span>
</template>

<script>
export default {
	name:'DropDownInput',
	props:['value'],
	data() {
	return { configSelected:"10" }
 }
}
</script>

<style scoped>
select.sel--main-blue { 
   border-radius:19px;
   border-style:solid;
   border-color:deepskyblue;
   background-color:deepskyblue;
   color:aqua;
   font-weight:bolder;
}
</style>