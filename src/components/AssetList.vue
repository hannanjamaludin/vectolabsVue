<template>
    <div>
        <h1>Asset List</h1>
        <table border="1">
            <thead>
                <tr>
                    <th>Asset Name</th>
                    <th>Department</th>
                </tr>
            </thead>
            <tbody>
                <tr v-for="(asset, index) in assets" :key="index">
                    <td>{{ asset.name }}</td>
                    <td>{{ asset.department }}</td>
                </tr>
            </tbody>
        </table>
        <button @click="downloadCSV">Download CSV</button>
    </div>
</template>

<script>
export default{
    data() {
        return {
            assets: [
                { name: "Printer", department: "HR" },
                { name: "Monitor", department: "IT" },
                { name: "Barcode Scanner", department: "ACCOUNT" },
            ],
        };
    },
    methods: {
        downloadCSV() {
            let csvContent = "data:text/csv;charset=utf-8,";
            csvContent += "Asset Name,Department\n";
            this.assets.forEach((asset) => {
                csvContent += `${asset.name},${asset.department}\n`;
            });
            const encodedUri = encodeURI(csvContent);
            const link = document.createElement("a");
            link.setAttribute("href", encodedUri);
            link.setAttribute("download", "assets.csv");
            document.body.appendChild(link);
            link.click();
        },
    },
};
</script>