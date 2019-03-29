<template>
    <div class="app">
        <h2>{{titulo}}</h2>
        <table>
            <thead>
                <th>
                    Multa
                </th>
                <th>
                    Dias atrasados
                </th>
                <th>
                    Juros
                </th>
                <th>
                    Total
                </th>
            </thead>
            <tbody>
                <tr v-show="totalPagar != ''">
                    <td >R${{multaAtraso}}</td>
                    <td >{{diasAtrasados}}</td>
                    <td >R${{jurosCalculado}}</td>
                    <td>R${{totalPagar}}</td>
                </tr>
            </tbody>
        </table>
    </div>
</template>
<script>
export default {
    name: "app",
    props:[
        'titulo',
        'multaAtraso',
        'diasAtrasados',
        'jurosCalculado',
        'totalPagar'
    ]
}

</script>
<style>
table{
    width: 100%;
}
</style>


