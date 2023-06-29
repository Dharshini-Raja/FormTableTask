<template>
    
    <div class="main">
        <Form1 :initialData="editItemData" @values="displayed($event)" @editStudent="saveItem" />
        <table >
            <thead>
                <th>Name</th>
                <th>Mobile Number</th>
                <th>Total</th>
                <th>Email</th>
                <th>Edit</th>
            </thead>
            <tbody>
                <tr  v-for="(item,index) in arr" :key="index">
              
                    <td :title="item.uname">{{ $filters.truncateName(item.uname,10) }}</td>
                    <td>{{ item.umobile }}</td>
                    <td :style="{backgroundColor: getTotalColor(item.utotal)}">{{ item.utotal }}</td>
                    <td >{{ item.uemail }}</td>
                    <td><button @click="editItem(item,index)">Edit</button></td>
                </tr>
                
            </tbody>
        </table>
    </div>
</template>
<script>
import Form1 from '@/components/Forms.vue';

export default{
    name:'Table1',
    components:{
        Form1
    },
    data(){
        return{ 
        arr: [],
        editItemData: null,
        editIndex:  null,
        hide: false}
    },
    methods:{
        displayed(data){
       let a=JSON.parse(data);
      this.arr.push(a);
     
       },editItem(item,index){
        this.editItemData = {...item};
        this.editIndex = index;
       },
       saveItem(formData){
       
       // const index = this.arr.findIndex((item) => item === this.editItemData);
        //this.arr.splice(this.editIndex,1,formData);
        this.arr[this.editIndex]=formData;
        this.editItemData = null;
       },


       getTotalColor(total){
        if(total>=85) return 'green';
        else if(total>=40) return 'blue';
        else return 'red';
       }


    }
}

 
</script>



<style>
table {
    border: solid 4px #000000;
    border-collapse: collapse;
    border-spacing: 0;
    font: normal 13px Arial, sans-serif;
    width: 100%
}
thead th {
    background-color: #476060;
    border: solid 4px #000000;
    color: #ffffff;
    padding: 30px;
    text-align: left;
    font-size: 20px;
    text-shadow: 1px 1px 1px #fff;
}
tbody td {
    border: solid 4px #000000;
    color: #f9f9f9;
    padding: 10px;
    font-size: 20px;
}
</style>