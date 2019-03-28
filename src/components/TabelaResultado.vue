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
                <tr>
                    <td>{{multaAtraso}}</td>
                    <td></td>
                    <td></td>
                    <td></td>
                </tr>
            </tbody>
        </table>
    </div>
</template>
<script>
export default {
    name: "app",
    props:{
        titulo:String,
        multaAtraso:Float32Array,
        diferencaDias: 
    }
}
</script>

