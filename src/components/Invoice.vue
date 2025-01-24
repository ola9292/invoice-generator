<script setup>
    import { ref, computed } from 'vue';
    import html2pdf from 'html2pdf.js' 

    const step = ref(1)
    //change step
    const preview = () => {
        step.value = 2
    }
    const goBack = () => {
        step.value = 1
    }
    const discount = ref(0);
    const bill_to = ref({
        name : null,
        address : null,
        company_address: null,
        email: null,  
    });
    const ship_to = ref({
        name : null,
        address : null,
        company_address: null,
        email: null,
    })
    const invoice = ref({
        date: null,
        invoice_no : null
    })
    const totalWithoutDiscount = ref(0)
    const items = ref([])
    //add item
    const addItem = () => {
        items.value.push({
            service:'',
            description:'',
            quantity:0,
            unit_price:0,
            total:0,
        })
    }
    //remove item
    const removeItem = (index) => {
        return items.value.splice(index, 1)
    }

    //validate inputs
    const validateInputs = () => {
        items.value.forEach((item) => {
            if(item.quantity < 0){
                item.quantity = 0
            }
            if (item.unit_price < 0) item.unit_price = 0;
        })
        if(discount.value < 0){
            discount.value = 0;
        }
    }

    //calculate total
    const calculateTotal = (index) => {
        const item = items.value[index]
        if (!item.quantity || item.quantity < 0) item.quantity = 0;
        if (!item.unit_price || item.unit_price < 0) item.unit_price = 0;
        const result = item.quantity * item.unit_price;
        item.total = result;
    }
    //calculate total
    const getTotal = computed(() => {
        let grandTotal = 0
        items.value.forEach((item) => {
            grandTotal += item.total
        })
        totalWithoutDiscount.value = grandTotal
        if (discount.value < 0){ discount.value} ; 
        let grandTotalSum = grandTotal - (grandTotal * (discount.value/100))
        return `£${grandTotalSum.toFixed(2)}`
    })

    // Add this new download pdf function
    const downloadPDF = () => {
        const element = document.getElementById('invoice-preview')
        
        const options = {
            margin: 1,
            filename: `invoice-${invoice.value.client_name}.pdf`,
            image: { type: 'jpeg', quality: 0.98 },
            html2canvas: { scale: 2 },
            jsPDF: { unit: 'in', format: 'letter', orientation: 'portrait' }
        }
        
        html2pdf().from(element).set(options).save()
    }
</script>

<template>
    <Transition name="slide-fade">
    <div v-if="step == 1" class="container">
        <div class="flex-container-col">
            <input class="input" type="date" v-model="invoice.date" placeholder="Name">
            <input class="input" type="number" v-model="invoice.invoice_no" placeholder="Invoice Number">
        </div>
        <h2>Billing Information</h2>
        <div class="flex-container-col">
            <input class="input" type="text" v-model="bill_to.name" placeholder="Name">
            <input class="input" type="text" v-model="bill_to.address" placeholder="Address">
            <input class="input" type="text" v-model="bill_to.company_address" placeholder="Company Address">
            <input class="input" type="email" v-model="bill_to.email" placeholder="Email">
        </div>

        <h2>Shipping Information</h2>
        <div class="flex-container-col">
            <input class="input" type="text" v-model="ship_to.name" placeholder="Name">
            <input class="input" type="text" v-model="ship_to.address" placeholder="Address">
            <input class="input" type="text" v-model="ship_to.company_address" placeholder="Company Address">
            <input class="input" type="email" v-model="ship_to.email" placeholder="Email">
        </div>
      
        <h2>Invoice Items</h2>
        <table>
            <tr>
                <th>Service</th>
                <th>Description</th>
                <th>Quantity</th>
                <th>Unit price</th>
                <th>Total</th>
                <th>Actions</th>
            </tr>
            <tr v-for="(item, index) in items" :key="index">
                <td><input type="text" v-model="item.service"></td>
                <td><input type="text" v-model="item.description"></td>
                <td><input type="text" v-model.number="item.quantity" @input="calculateTotal(index)" @blur="validateInputs"></td>
                <td><input type="text" v-model.number="item.unit_price" @input="calculateTotal(index)" @blur="validateInputs"></td>
                <td>{{ item.total }}</td>
                <td><button @click="removeItem(index)">remove</button></td>
            </tr>
        </table>
        <button class="btn" @click="addItem">add item</button>

        <h2>Invoice Summary</h2>
        <label for="">Discount Amount: </label>
        <input type="number" v-model="discount" @blur="validateInputs">
        <p v-if="discount < 0" style="color: red;">Discount cannot be negative!</p>

        <div>
            <h2>Total Amount</h2>
            <h3>{{ getTotal }}</h3>
            
        </div>

        <div class="preview">
            <button class="btn" @click="preview" v-if="step == 1">see preview</button>
        </div>
       
       
    </div>
</Transition>
<Transition name="slide-fade-reverse">
    <div v-if="step == 2">
        <div class="container-2">
            
            <div id="invoice-preview">
                <div class="date_no preview">
                    <p v-if="invoice.date"><bold>Date:</bold> {{ invoice.date }}</p>
                    <p v-if="invoice.invoice_no"><bold>Invoice No:</bold> {{ invoice.invoice_no }}</p>
                </div>
                <div class="flex-container-row">
                   <div>
                    <h2>Bill To</h2>
                    <p>{{ bill_to.name }}</p>
                    <p>{{ bill_to.email }}</p>
                    <p>{{ bill_to.address }}</p>
                    <p>{{ bill_to.company_address }}</p>
                   </div>
                   <div>
                    <h2>Ship To</h2>
                    <p>{{ ship_to.name }}</p>
                    <p>{{ ship_to.email }}</p>
                    <p>{{ ship_to.address }}</p>
                    <p>{{ ship_to.company_address }}</p>
                   </div>
                </div>
                <h2>Invoice</h2>
                <p>{{ invoice.client_name }}</p>
                <p>{{ invoice.client_address }}</p>

                <table>
                    <tr>
                        <td>Service</td>
                        <td>Description</td>
                        <td>Quantity</td>
                        <td>Unit price</td>
                        <td>Total</td>
                    </tr>
                    <tr v-for="(item, index) in items" :key="index">
                        <td>{{ item.service }}</td>
                        <td>{{ item.description }}</td>
                        <td>{{ item.quantity }}</td>
                        <td>{{ item.unit_price }}</td>
                        <td>{{ item.total }}</td>
                    </tr>
                </table>
                <div class="summary">
                    <p>paid: £0</p>
                    <p>Subtotal: {{ totalWithoutDiscount }}</p>
                    <p>Discount: {{  `${discount}%`}}</p>
                    <p>Total to pay: {{ getTotal }}</p>
                </div>
            </div>
            
            <div class="flex-container-row">
            <button class="btn" @click="goBack" v-if="step == 2">back</button>
            <button class="btn" v-if="step == 2 && items.length > 0" @click="downloadPDF">Download PDF</button>
            
            </div>
        </div>
    </div>
  </Transition>
   
    
</template>

<style scoped>
    table {
    font-family: arial, sans-serif;
    border-collapse: collapse;
    width: 100%;
    margin-bottom: 10px;
    }

    td, th {
    border: 1px solid #dddddd;
    text-align: left;
    padding: 8px;
    }
    .container{
        overflow-x: auto;
        margin: auto;
        padding: 20px;
        width: 90%;
        max-width: 900px;
        box-shadow: rgba(0, 0, 0, 0.35) 0px 5px 15px;
    }
    .container-2{
        overflow-x: auto;
        padding: 20px;
    }
    .flex-container-col{
        display: flex;
        flex-direction: column;
        gap: 10px;
    }
    .flex-container-row{
        display: flex;
        gap: 10px;
        justify-content: space-between;
    }
    .input{
        padding: 8px;
    }
    .btn{
        padding: 8px 16px;
        border: none;
        background-color: #009e74;
        color: white;
        text-transform: capitalize;
    }
    .preview, .date_no{
        display: flex;
        justify-content: flex-end;
    }
    .date_no{
        flex-direction: column;
        align-items: flex-end;
    }
    .summary{
        margin: 15px 0;
        display: flex;
        flex-direction: column;
        align-items: flex-end;
        justify-content: flex-end;
        gap:10px
    }
    .summary > p{
        margin: 0;
    }
    /*
  Enter and leave animations can use different
  durations and timing functions.
*/
.slide-fade-enter-active {
  transition: all 0.3s ease-out;
}

.slide-fade-leave-active {
  transition: all 0.8s cubic-bezier(1, 0.5, 0.8, 1);
}

.slide-fade-enter-from,
.slide-fade-leave-to {
  transform: translateX(20px);
  opacity: 0;
}

/*
  Enter and leave animations for reverse direction
  with new class names.
*/
.slide-fade-reverse-enter-active {
  transition: all 0.3s ease-out;
}

.slide-fade-reverse-leave-active {
  transition: all 0.8s cubic-bezier(1, 0.5, 0.8, 1);
}

.slide-fade-reverse-enter-from,
.slide-fade-reverse-leave-to {
  transform: translateX(-50px); /* Opposite direction */
  opacity: 0;
}

</style>