<template>
<div id="filtmain__el">
<input id="filtround__el" placeholder="Filter by author" v-model="filterres">
<slot> Filtering by &quot;{{filterres}}&quot;</slot>
</div>
</template>


<script>
export default {
    name:'FilteringListLayout',
    props: {
        title: String
    },
    data() {
        return {
            filterres:""
        }
    }

}
</script>

<style scoped>
#filtmain__el {
margin:5px;
display:block;
}

input#filtround__el {
border-radius:25px;
color:#0bd74d;
}

</style>