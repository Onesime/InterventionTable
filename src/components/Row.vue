<template>
    <tr>
        <td>{{ row.id}}</td>
        <td>{{ row.first_name}}</td>
        <td>{{ row.last_name}}</td>
        <td>{{ row.email}}</td>
        <td>{{ row.title}}</td>
        <td>{{ row.place}}</td>
        <td></td>
    </tr>
</template>

<script>

export default {
    name: 'Row',
    props: [
        'row'
    ],
}

</script>
