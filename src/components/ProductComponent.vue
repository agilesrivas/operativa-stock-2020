
<template>
  
  <div class="content">
    <div id="form-container" class="__col __col-3 __align-self-center">
      <div class="__card" v-if="loading">
        <header class="__form-header">
          <h2 class="__title">Producto</h2>
        </header>
        <div class="__form-body">
          <div class="__loading-container __text-center">
            <i class="fas fa-spinner fa-spin"></i> Loading
          </div>
        </div>
      </div>

      <div v-else>
        <form action="" class="row text-white div_trans8 corner4 p-2" v-if="form == 'create'">
          <div class="row">
            <div class="col-md-12">
            <h2 class="">Producto</h2>
            <h6 class="">Agrega un nuevo producto</h6>
            </div>
            <div class="col-md-3 form-group form-inline">
              <label for="product_name">Nombre: </label>
              <input id="product_name" type="text" required placeholder=" " v-model.trim="product.name">
            </div>
            <div class="col-md-3 form-group form-inline">
              <label for="product_cost">Costo: </label>
              <input id="product_cost" type="number" required placeholder=" " v-model.number="product.cost">
            </div>
            
            <div class="col-md-3 form-group form-inline">
              <label for="product_code">Código: </label>
              <input id="product_code" type="text" required placeholder=" " v-model.trim="product.code">
            </div>
            <div class="col-md-3 form-group form-inline">
              <label for="product_amount">Demanda diaria: </label>
              <input id="product_amount" type="number" required placeholder=" " v-model.number="product.amount" @blur="demandaOnChange()">
            </div>
             <div class="col-md-3 form-group form-inline">
              <label for="stock_actual">Stock: </label>
              <input id="stock_actual" type="number" required placeholder=" " v-model.number="product.currentAmount">
            </div>
            <div class="col-md-3 form-group form-inline">
              <label for="product_category">Categoría: </label>
              <select id="product_category" required v-model="product.category">
                <option value="" selected disabled>Elige una</option>
                <option :value="categoryUnit" v-for="(categoryUnit, index) in categories" :key="index">{{ categoryUnit.name }}</option>
              </select>
            </div>
              <div class="col-md-3 form-group form-inline">
                <input type="checkbox" name="model" id="model-p"  v-model="check">
                <label for="model-p"> Viene mi proveedor</label>
              </div>
            <div class="col-md-3 form-group form-inline" v-if="check">
              <label for="product_provider">Proveedor: </label>
              <select id="product_provider" v-model="product.provideer">
                <option value="" selected disabled>Elige una</option>
                <option :value="providerUnit" v-for="(providerUnit, index) in providers" :key="index">{{ providerUnit.name }}</option>
              </select>
            </div>
            <div class="col-md-3 form-group form-inline">
              <label for="product_zone">Zona: </label>
              <select id="product_zone" v-model="product.zone">
                <option disabled value="">Seleccione una</option>
                <option>A</option>
                <option>B</option>
                <option>C</option>
              </select>
            </div>

            <div class="col-md-12 form-group form-inline">
            <div class="__message __message-success __mb-1" v-if="success">
              {{ success }}
            </div>
            <div class="__message __message-danger __mb-1" v-else-if="error">
              {{ error }}
            </div>
            <div class="col-md-6 form-group form-inline">
              <a href="" class="btn btn-info" @click.prevent="create">Agregar</a>            
              <a href="" class="btn btn-outline-light ml-3" @click.prevent="clean">Limpiar campos</a>
            </div>
          </div>
          </div>
        </form>

        <form action="" class="row text-white div_trans8 corner4 p-2" v-else-if="form == 'update'">
          <div class="row">
            <div class="col-md-12">
            <h2 class="__title">Producto</h2>
            <p class="__description">Modifica un producto existente</p>
          </div>
            <!-- <div class="col-md-3 form-group form-inline">
              <label for="category_id">ID: </label>
              <input id="category_id" type="number" required placeholder=" " v-model.number="product.id" disabled>
            </div> -->
            <div class="col-md-3 form-group form-inline">
              <label for="product_name">Nombre: </label>
              <input id="product_name" type="text" required placeholder=" " v-model.trim="product.name">
            </div>
            <div class="col-md-3 form-group form-inline">
              <label for="product_amount">Demanda diaria: </label>
              <input id="product_amount" type="number" required placeholder=" " v-model.number="product.amount">
            </div>
            <div class="col-md-3 form-group form-inline">
              <label for="product_cost">Costo: </label>
              <input id="product_cost" type="number" required placeholder=" " v-model.number="product.cost">
            </div>
          
            <div class="col-md-3 form-group form-inline">
              <label for="product_code">Código: </label>
              <input id="product_code" type="text" required placeholder=" " v-model.trim="product.code">
            </div>
            <div class="col-md-3 form-group form-inline">
              <label for="stock_actual">Stock: </label>
              <input id="stock_actual" type="number" required placeholder=" " v-model.number="product.currentAmount">
            </div>
            <div class="col-md-3 form-group form-inline">
              <label for="product_category">Categoría: </label>
              <select id="product_category" required v-model="product.category">
                <option value="" selected disabled>Elige una</option>
                <option :value="categoryUnit" v-for="(categoryUnit, index) in categories" :key="index">{{ categoryUnit.name }}</option>
              </select>
            </div>
            <div class="col-md-3 form-group form-inline">
              <label for="product_provider">Proveedor: </label>
              <select id="product_provider" v-model="product.provideer">
                <option value="" selected disabled>Elige una</option>
                <option :value="providerUnit" v-for="(providerUnit, index) in providers" :key="index">{{ providerUnit.name }}</option>
              </select>
            </div>
            <div class="col-md-3 form-group form-inline">
              <label for="product_zone">Zona: </label>
              <select id="product_zone" v-model="product.zone">
                <option disabled value="">Seleccione una</option>
                <option>A</option>
                <option>B</option>
                <option>C</option>
              </select>
            </div>

            <div class="col-md-12 form-group form-inline">
              <div class="__message __message-success __mb-1" v-if="success">
                {{ success }}
              </div>
              <div class="__message __message-danger __mb-1" v-else-if="error">
                {{ error }}
              </div>
              <div class="col-md-3 form-group form-inline">
                <a href="" class="btn btn-info"  @click.prevent="update">Modificar</a>
                <a href="" class="btn btn-outline-light ml-3" @click.prevent="clean">Limpiar campos</a>
              </div>
              <div class="col-md-3 form-group form-inline">
                <a href="" class="btn btn-outline-success" @click.prevent="triggerForm(-1)">Quiero crear</a>
            </div>
            </div>            
          </div>
        </form>
      </div>
    </div>

<div class="row mt-3">
    <div class="content ">
      <div id="table-container" class="__card __max-full-height-perc">
        <table id="table" class="__table __full-width-perc __text-center __table-bordered __table-hoverrable">
          <thead>
            <tr>
              <th>Nombre</th>  
              <th>Costo</th>
              <th>Código</th>
              <th>Demanda diaria</th>
              <th>Stock</th>
              <th>Punto de Reorden</th>
              <th>Lead Time</th>
              <th>Categoría</th>
              <th>Proveedor</th>
              <th>Zona</th>
              <th colspan="2">Extra</th>
            </tr>
          </thead>
          <tbody>
            <tr v-for="(tock, index) in stocks" :key="index">
              <td> {{ tock.name }} </td>
              <td> {{ tock.cost }} </td>
              <td> {{ tock.code }} </td>
              <td> {{ tock.amount }} </td>
              <td> {{ tock.currentAmount}} </td>
              <td> {{ tock.reorder_point}} </td>
              <td v-if="tock.provideer!==null"> {{ tock.provideer.leadtime }} </td>
              <td v-else>{{diasDeCompras}}</td>
              <td> {{ tock.category.name }} </td>
              <td v-if="tock.provideer!==null"> {{ tock.provideer.name }} </td>
              <td v-else></td>
              <td>{{ tock.zone }}</td>
              <td>
                <button class="__button __button-warning __button-rounded fas fa-pencil-alt" :id="tock.id+'-edit'" @click="triggerForm(tock.id)" :value="tock.id"></button>
              </td>
              <td>
                <button class="__button __button-danger __button-rounded fas fa-times" :id="tock.id+'-remove'" @click="remove(tock.id)" :value="tock.id"></button>
              </td>
            </tr>
          </tbody>
        </table>
      </div>
    </div>
  </div>
    </div>

</template>

<script>
/* eslint-disable */
import CategoryService from '@/services/CategoryService'
import ProviderService from '@/services/ProviderService'
import ProductService from '@/services/ProductService'
import ConfigService from '@/services/ConfigService'

export default {
  name: 'ProductComponent',
  data() {
    return {
        product: {
        id: 0,
        name: '',
        amount: 0,
        cost: 0,
        code: '',
        category: '',
        provideer: '',
        currentAmount:0,
        reorder_point:0,
        zone:'',
                },
      check:false,
      success: '',
      error: '',
      loading: false,
      form: 'create',
      providers: [],
      categories: [],
      stocks: [],
      diasDeCompras: ''
    }
  },
  methods: {
    create() {
      if ( this.product.name.trim() && this.product.amount >= 0 && this.product.cost >= 0  && this.product.code.trim() &&  this.product.category ) {
     let product=null;
      if(this.check){
          product={
                  name: this.product.name,
                  amount: this.product.amount,
                  cost: this.product.cost,
                  code: this.product.code,
                  category: this.product.category,
                  provideer: this.product.provideer,
                  currentAmount:this.product.currentAmount,
                  reorder_point:this.product.reorder_point,
                  zone: this.product.zone
            }
            console.log(product);
      }else{
        
          product={
                  name: this.product.name,
                  amount: this.product.amount,
                  cost: this.product.cost,
                  code: this.product.code,
                  provideer:null,
                  category: this.product.category,
                  currentAmount:this.product.currentAmount,
                  reorder_point:this.product.reorder_point,
                  zone: this.product.zone
            }
      }
            
            ProductService.create(product)
            .then(resolve => {            
               this.success="Cargado Exitosamente";
            ProductService.retrieveAll()
            .then((response)=>{
              this.stocks=response;
              this.clean();
            })
            .catch((error)=>{
              console.log(error);
            });
            setTimeout(() => {
              this.success = undefined
            }, 2500)
            this.clean()
          })
          .catch(reject => {
            this.error = reject

            setTimeout(() => {
              this.error = undefined
            }, 2500)
          }) 
      } else {
        this.error = 'Llene todos los campos.'

        setTimeout(() => {
          this.error = undefined
        }, 2500)
      }
    },
    remove(id) { 
      const target = document.getElementById(id + "-remove");
      target.disabled = true
      target.classList.remove('fa-times')
      target.classList.add('fa-sync')
      target.classList.add('fa-spin')

      ProductService.remove(id)
        .then(resolve => {
          target.classList.remove('fa-sync')
          target.classList.remove('fa-spin')
          target.classList.add('fa-times')
          target.disabled = false 
          ProductService.retrieveAll().then((response)=>{
              this.stocks=response;
            }).catch((error)=>{
              console.log(error);
            });
        }).catch((error)=>{
          console.log(error);
        });
    },
    update() {
      if ( this.product.id > 0 && this.product.amount >= 0 && this.product.cost >= 0  && this.product.code.trim() &&  this.product.category ) {
         
        let product = {
                  id: this.product.id,
                  name: this.product.name,
                  amount: this.product.amount,
                  cost: this.product.cost,
                  code: this.product.code,
                  category: this.product.category,
                  provideer: this.product.provideer,
              currentAmount:this.product.currentAmount,
              reorder_point:this.product.reorder_point,
              zone: this.product.zone
            } 
            ProductService.update(product)
              .then(resolve => {
                this.success = "Modificado Exitosamente"
            ProductService.retrieveAll().then((resolve)=>{
              this.stocks=resolve;
              this.clean();
            }).catch((error)=>{
              console.log(error);
            });
            setTimeout(() => {
              this.success = undefined
            }, 2500)
          })
          .catch(reject => {
            this.error = reject

            setTimeout(() => {
              this.error = undefined
            }, 2500)
          })
      } else {
        this.error = 'Llene todos los campos.'

        setTimeout(() => {
          this.error = undefined
        }, 2500)
      } 
     
    },
    async triggerForm(id) {
      const target = document.getElementById(id + "-edit");

      if (id === -1) {
        this.loading = true;
        this.form = 'create';
        this.clean();
        this.loading = false;

      } else {
        target.disabled = true;
        target.classList.remove('fa-edit');
        target.classList.add('fa-sync');
        target.classList.add('fa-spinner');

        const resolve = await ProductService.retrieve(id);
        this.product=resolve;
        
        target.classList.remove('fa-sync');
        target.classList.remove('fa-spinner');
        target.classList.add('fa-edit');
        target.disabled = false;

        this.form = 'update';
        this.loading = false;
      }
    },
    clean() {
      this.product.id=0
      this.product.name = ''
      this.product.amount = 0
      this.product.cost = 0
      this.product.code = ''
      this.product.currentAmount=0
      this.product.category = ''
      this.product.provideer = ''
      this.product.zone = ''
    },
    demandaOnChange() {
      if (this.product.amount !== "" && this.product.cost !== ""){
        console.log(this.product.amount);
        console.log(this.product.cost);
        let cav = this.product.amount * this.product.cost * 365;
        if (cav > 1000000){
          this.product.zone = 'C';
        }else if(cav < 1000000 && cav > 800000)
          this.product.zone = 'B';
        else{
          this.product.zone = 'A';
        }     
        console.log(cav);
        console.log(this.product.zone);
      }
    }
  },
  created() {
    CategoryService.retrieveAll()
      .then(resolve => {
        this.categories = resolve     
      })
    
    ProviderService.retrieveAll()
      .then(resolve => {
        this.providers = resolve        
      })

    ConfigService.retrieve(1).then((response) => {
      this.diasDeCompras = response.diasDeCompras;
    })

    ProductService.retrieveAll()
      .then(resolve => {
        this.stocks = resolve
      })
  },
  mounted() {
    const table_container = document.getElementById('table-container'),
      table = document.getElementById('table'),
      table_container_height = table_container.clientHeight,
      table_height = table.clientHeight;

    if (table_container_height <= table_height) {
      table_container.parentElement.classList.remove('__align-self-center')
      table_container.classList.add('__overflow-scroll-y')
    } else {
      table_container.parentElement.classList.add('__align-self-center')
      table_container.classList.remove('__overflow-scroll-y')
    }
  }
}
</script>