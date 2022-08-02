<template>
<div class="container">
    <div>
        <input type="text" v-model.trim="newData.userName" placeholder="Enter UserName"/>
        
        <select v-model="newData.Gender">
            <option disabled value="">Select Gender</option>
            <option>Male</option>
            <option>Female</option>
        </select>
        <input type="button" value="Add" @click="addList()"/>
    </div>
    <div>
        Fitler: 
        <button @click="filterMode = 'All'">All</button>
        <button @click="filterMode = 'Male'">Male</button>
        <button @click="filterMode = 'Female'">Female</button>
    </div>
    <table class="table">
        <thead>
            <tr>
                <td>User ID</td>
                <td>User Name</td>
                <td>Gender</td>
                <td></td>
            </tr>
        </thead>
        <tbody>
            <tr v-for="item in filteredList" :key="item.id">
                <td>
                    <div>{{ item.id }}</div>
                </td>
                <td>
                    <div v-if="item.Status === 'Display'">{{ item.userName }}</div>
                    <div v-if="item.Status === 'Edit'">
                        <input type="text" v-model.trim="item.userName" placeholder="Enter UserName"/>
                    </div>
                </td>
                <td>
                    <div v-if="item.Status === 'Display'">{{ item.Gender }}</div>
                    <div v-if="item.Status === 'Edit'">
                        <select v-model="item.Gender">
                            <option disabled value="">Select Gender</option>
                            <option>Male</option>
                            <option>Female</option>
                        </select>
                    </div>
                </td>
                <td>
                    <div v-if="item.Status === 'Display'">
                        <button @click="editItem(item)">∴</button>
                        <button @click="removeItem(item.id)">&times;</button>
                    </div>

                    <div v-if="item.Status === 'Edit'">
                        <button @click="updateItem(item)">☑</button>
                        <button @click="editCancel(item)">&times;</button>
                    </div>
                </td>
            </tr>
        </tbody>
        <tfoot>
            <tr>
                <td colspan="4">
                    {{ filteredList.length }} users
                </td>
            </tr>
        </tfoot>
    </table>
</div>
</template>

<script>
export default{
    name: 'todo-list',
    data () {
        return{
            newData:{
                id: 0,
                userName: '',
                Gender: '',
                Status: 'Display'
            },
            filterMode: 'All',
            editTitleCache: '',
            userData: [
                {
                    id: 1,
                    userName: 'Collin',
                    Gender: 'Male',
                    Status: 'Display'
                },
                {
                    id: 2,
                    userName: 'Jun',
                    Gender: 'Male',
                    Status: 'Display'
                },
                {
                    id: 3,
                    userName: 'Terresa',
                    Gender: 'Female',
                    Status: 'Display'
                },
                {
                    id: 4,
                    userName: 'Joma',
                    Gender: 'Male',
                    Status: 'Display'
                },
                {
                    id: 5,
                    userName: 'Helen',
                    Gender: 'Female',
                    Status: 'Display'
                },
                {
                    id: 6,
                    userName: 'Kevin',
                    Gender: 'Male',
                    Status: 'Display'
                },
            ]
        }
    },
    methods:{
        addList(){
            if (this.newData.userName === ''){
                alert('Please Enter UserName');
                return;
            }
            if (this.newData.Gender === ''){
                alert('Please Select a Gender');
                return;
            }

            this.userData.push({
                id: Math.max(...this.userData.map(item => item.id)) + 1,
                userName: this.newData.userName,
                Gender: this.newData.Gender,
                Status: 'Display'
            });

            this.newData.userName = '';
            this.newData.Gender = '';
        },
        removeItem(id){
            if(confirm('Are you sure?'))
                this.userData = this.userData.filter(item => item.id !== id);
        },
        editItem(item){
            this.editTitleCache = Object.assign({}, item);
            this.userData.forEach(item => item.Status = 'Display');
            item.Status = 'Edit';
        },
        editCancel(item){
            item.userName = this.editTitleCache.userName;
            item.Gender = this.editTitleCache.Gender;
            item.Status = 'Display';
        },
        updateItem(item){
            item.Status = 'Display';
        }
    },
    computed: {
        filteredList(){
            if ( this.filterMode == 'All'){
                return this.userData;
            }
            else{
                return this.userData.filter(item => item.Gender == this.filterMode)
            }
        }
    }
}
</script>

<style>
    .container{
        max-width: 720px;
        margin: auto;
    }

     .container table{
        width: 100%;
    }

     .container table thead tr{
        background-color: #ddd;
    }
</style>