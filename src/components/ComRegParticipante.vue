<template>
 <div>

   <!-- version 20210302 version 1.5 -->
        <b-card bg-variant="dark" text-variant="white" title="REPORTE FÁCIL THS ">
      <b-card-text>
        Bienvenido a tu reporte de profesional independiente. 
      </b-card-text>
      <b-button style="margin: 10px" size="sm" variant="success" v-b-modal.modalInsercion  @click="SetBanderaFormulario(1)" class="bg-info text-white" >Ingresar Personal a reportar</b-button>
    </b-card>

    <table  class="table-responsive sm">
    <thead>
        <tr>
             <p>
                <b-alert show variant="danger">Entidad en session: {{userLogged.entidad + ' -- '+ this.NombreEntidad}}</b-alert>
            </p>
        </tr>
        <tr>
          <h3>Total Registros: {{this.PersonasEntidad.length}}</h3>
        </tr>
    </thead>
    </table> 
  

 <div id="modal2">
    <b-modal
      id="modalInsercion"
      size= 'lg'
      ref="modal2"
      title= "REGISTRO DE PERSONAL A REPORTAR"
      valor= item.Id_Curso     
      @ok="onSubmit"
    >
    <b-form @submit.stop.prevent="onSubmit"> 

    <p v-if="errors.length">
   <!--  <b>Por favor, corrija el(los) siguiente(s) error(es):</b> -->
    <b-alert show variant="danger">Por favor, corrija el(los) siguiente(s) error(es):</b-alert>
    <ul>
       <li v-for="error in errors" :key="error">{{ error }}</li>
    </ul>
    </p>

    <table>
        <tr>            
            <td colspan="2">
 
                 <b-form-group id="group-0" label-for="input-0">
                <b-input-group prepend="Es reporte de personal de apoyo logístico?" class="mb-2 mr-sm-2 mb-sm-0"> 
                <b-form-select
                id="input-0"
                name="input-0"
                v-model="$v.form.EsThs.$model"
                :options="EsThs"
                :state="validateState('EsThs')"
                aria-describedby="input-0-live-feedback"
                ></b-form-select>
                <b-form-invalid-feedback  id="input-0-live-feedback">Por favor seleccione una opción válida</b-form-invalid-feedback>
                </b-input-group> 
                </b-form-group>
                
            </td>
         <tr>            
           <td>
                <b-form-group id="group-3" label-for="input-3">
                <b-input-group prepend="Código Entidad:" class="mb-2 mr-sm-2 mb-sm-0"> 
                <b-form-input
                id="input-3"
                name="input-3"
                v-model= this.CodEnti
                :disabled="true"
                :state="validateState('codentidad')"
                aria-describedby="input-3-live-feedback"
                ></b-form-input>
                <b-form-invalid-feedback  id="input-3-live-feedback">Requerido solo 10 caracteres</b-form-invalid-feedback>
                </b-input-group> 
                </b-form-group> 
            </td>
            <td>
                 <b-form-group id="group-4" label-for="input-4">
                <b-input-group prepend="Nombre Entidad:" class="mb-2 mr-sm-2 mb-sm-0">
                <b-form-input
                id="input-4"
                name="input-4"
                v-model="$v.form.nomentidad.$model"
                :state="validateState('nomentidad')"
                aria-describedby="input-4-live-feedback"
                ></b-form-input>
                <b-form-invalid-feedback id="input-4-live-feedback">Nombre Entidad Requerido</b-form-invalid-feedback>
                </b-input-group> 
                </b-form-group>
            </td>
        </tr>  			
        <tr>            
           <td>
                <b-form-group id="group-1" label-for="input-1">
                <b-input-group prepend="Tipo Documento:" class="mb-2 mr-sm-2 mb-sm-0"> 
                <b-form-select
                id="input-1"
                name="input-1"
                v-model="$v.form.tipoid.$model"
                :options="TiposId"
                :state="validateState('tipoid')"
                aria-describedby="input-1-live-feedback"
                ></b-form-select>
                <b-form-invalid-feedback  id="input-1-live-feedback">Tipo Id Requerido</b-form-invalid-feedback>
                </b-input-group> 
                </b-form-group>
            </td>
            <td>
                <b-form-group id="group-2" label-for="input-2">
                <b-input-group prepend="Nro Documento:" class="mb-2 mr-sm-2 mb-sm-0">
                <b-form-input
                id="input-2"
                name="input-2"
                v-model="$v.form.nroid.$model"
                :state="validateState('nroid')"
                aria-describedby="input-2-live-feedback"
                ></b-form-input>
                <b-form-invalid-feedback id="input-2-live-feedback">Requerido mas de 3 números</b-form-invalid-feedback>
                </b-input-group> 
                </b-form-group>
            </td>
        </tr>
         <tr>            
           <td>
                <b-form-group id="group-5" label-for="input-5">
                <b-input-group prepend="Primer Apellido:" class="mb-2 mr-sm-2 mb-sm-0"> 
                <b-form-input
                id="input-5"
                name="input-5"
                v-model="$v.form.papellido.$model"
                :state="validateState('papellido')"
                aria-describedby="input-5-live-feedback"
                ></b-form-input>
                <b-form-invalid-feedback  id="input-5-live-feedback">Requerido minimo 3 letras</b-form-invalid-feedback>
                </b-input-group> 
                </b-form-group>
            </td>
            <td>
                <b-form-group id="group-6" label-for="input-6">
                <b-input-group prepend="Segundo Apellido:" class="mb-2 mr-sm-2 mb-sm-0">
                <b-form-input
                id="input-6"
                name="input-6"
                v-model="$v.form.sapellido.$model"
                :state="validateState('sapellido')"
                aria-describedby="input-6-live-feedback"
                ></b-form-input>
                <b-form-invalid-feedback id="input-6-live-feedback">Segundo apellido inválido</b-form-invalid-feedback>
                </b-input-group> 
                </b-form-group>
            </td>
        </tr>      
        <tr>            
           <td>
                <b-form-group id="group-7" label-for="input-7">
                <b-input-group prepend="Primer Nombre:" class="mb-2 mr-sm-2 mb-sm-0"> 
                <b-form-input
                id="input-7"
                name="input-7"
                v-model="$v.form.pnombre.$model"
                :state="validateState('pnombre')"
                aria-describedby="input-7-live-feedback"
                ></b-form-input>
                <b-form-invalid-feedback  id="input-7-live-feedback">Requerido minimo 3 letras</b-form-invalid-feedback>
                </b-input-group> 
                </b-form-group>
            </td>
            <td>
                <b-form-group id="group-8" label-for="input-8">
                <b-input-group prepend="Segundo Nombre:" class="mb-2 mr-sm-2 mb-sm-0">
                <b-form-input
                id="input-8"
                name="input-8"
                v-model="$v.form.snombre.$model"
                :state="validateState('snombre')"
                aria-describedby="input-8-live-feedback"
                ></b-form-input>
                <b-form-invalid-feedback id="input-8-live-feedback">Segundo nombre inválido</b-form-invalid-feedback>
                </b-input-group> 
                </b-form-group>
            </td>
        </tr> 
        <tr>
           <td>
                <b-form-group id="group-9" label-for="input-9">
                <b-input-group prepend="Municipio:" class="mb-2 mr-sm-2 mb-sm-0"> 
                <b-form-select
                id="input-9"
                name="input-9"
                v-model="$v.form.municipio.$model"
                :options="Municipios"
                :state="validateState('municipio')"
                aria-describedby="input-9-live-feedback"
                ></b-form-select>
                <b-form-invalid-feedback  id="input-9-live-feedback">Municipio es Requerido</b-form-invalid-feedback>
                </b-input-group> 
                </b-form-group>
            </td>
            <td>
                <b-form-group id="group-10" label-for="input-10" v-show="$v.form.EsThs.$model">
                <b-input-group prepend="Perfil Profesional:" class="mb-2 mr-sm-2 mb-sm-0">
                <b-form-select
                id="input-10"
                name="input-10"
                v-model="perfil"
                :options="Perfil"    
                ></b-form-select>
                </b-input-group> 
                </b-form-group> 
            </td>
        </tr>   
        <tr>
           <td>
                <b-form-group id="group-11" label-for="input-11">
                <b-input-group prepend="Servicio:" class="mb-2 mr-sm-2 mb-sm-0"> 
                <b-form-select
                id="input-11"
                name="input-11"
                v-model="$v.form.servicio.$model"
                :options="Servicio"
                :state="validateState('servicio')"
                aria-describedby="input-11-live-feedback"
                ></b-form-select>
                <b-form-invalid-feedback  id="input-11-live-feedback">Servicio es Requerido</b-form-invalid-feedback>
                </b-input-group> 
                </b-form-group>
            </td>
            <td>
                <b-form-group id="group-12" label-for="input-12">
                <b-input-group prepend="Área Covid:" class="mb-2 mr-sm-2 mb-sm-0">
                <b-form-select
                id="input-12"
                name="input-12"
                v-model="$v.form.areacovid.$model"
                :options="AreaCovid"
                :state="validateState('areacovid')"
                aria-describedby="input-12-live-feedback"
                ></b-form-select>
                <b-form-invalid-feedback id="input-12-live-feedback">Área Covid es Requerido</b-form-invalid-feedback>
                </b-input-group> 
                </b-form-group>
            </td>
        </tr> 
        <tr>
           <td>
                <b-form-group id="group-13" label-for="input-13">
                <b-input-group prepend="Dedicación:" class="mb-2 mr-sm-2 mb-sm-0"> 
                <b-form-select
                id="input-13"
                name="input-13"
                v-model="$v.form.dedicacion.$model"
                :options="Dedicacion"
                :state="validateState('dedicacion')"
                aria-describedby="input-13-live-feedback"
                ></b-form-select>
                <b-form-invalid-feedback  id="input-13-live-feedback">Dedicación es Requerido</b-form-invalid-feedback>
                </b-input-group> 
                </b-form-group>
            </td>
            <td>
                <b-form-group id="group-14" label-for="input-14">
                <b-input-group prepend="Cargo:" class="mb-2 mr-sm-2 mb-sm-0">
                <b-form-select
                id="input-14"
                name="input-14"
                v-model="$v.form.cargo.$model"
                :options= this.LoadCargo
                :state="validateState('cargo')"
                aria-describedby="input-14-live-feedback"
                ></b-form-select>
                <b-form-invalid-feedback id="input-14-live-feedback">Cargo es Requerido</b-form-invalid-feedback>
                </b-input-group> 
                </b-form-group>
            </td>
        </tr> 
         <tr>
           <td>
                <b-form-group id="group-15" label-for="input-15">
                <b-input-group prepend="Ind Actualización:" class="mb-2 mr-sm-2 mb-sm-0"> 
                <b-form-select
                id="input-15"
                name="input-15"
                v-model="$v.form.indactualizacion.$model"
                :options="Indicador"
                :state="validateState('indactualizacion')"
                aria-describedby="input-15-live-feedback"
                ></b-form-select>
                <b-form-invalid-feedback  id="input-15-live-feedback">Indicador Actualización es Requerido</b-form-invalid-feedback>
                </b-input-group> 
                </b-form-group> 
            </td>
        </tr>                                              
    </table>

    <!--   <b-button type="submit" variant="primary">Guardar</b-button> -->
      <b-button class="ml-2" @click="resetForm()">Limpiar</b-button>
    </b-form>
    </b-modal>
 </div> 

   <div>
    <b-table striped hover responsive sticky-header head-variant="light" :items="LlenarGrillaPersonas" :fields="fields">
     <template v-slot:cell(Acciones_de_tabla)="data" >
       <b-button size="sm" variant="outline-danger" class="mr-2" @click=EliminarParticipante(data.item.id)>Eliminar</b-button>
       <b-button size="sm" variant="outline-success" v-b-modal.modalInsercion class="mr-2" @click="EditarParticipante(data.item.id,data.item.TipoRegistro,data.item.TipoId,data.item.NroId,data.item.PrimerApellido,data.item.SegundoApellido,data.item.PrimerNombre,data.item.SegundoNombre,data.item.CodigoMunicipio,data.item.CodigoPerfil,data.item.CodigoEntidad,data.item.NombreEntidad,data.item.CodigoServicio,data.item.CodigoAreaCovid,data.item.CodigoDedicacion,data.item.CodigoCargo,data.item.IndicadorActualizacion,data.item.FechaCorte,2)" >Editar</b-button>
     </template>
    </b-table>
  </div> 

    <b-button variant="success" @click="EnviarPago()">Realiza el pago AQUI Y habilita el enlace de descarga</b-button>
    <b-button style="margin: 10px" size="sm" variant="success" v-b-modal.modalInsercion  @click="SetBanderaFormulario(1)" class="bg-info text-white" >Ingresar otra persona </b-button>

      <div v-if="this.CodTransaccion > 0"><b-alert show variant="info"> {{this.DescripcionTransaccion}}  </b-alert></div>

    <div v-if="this.CodTransaccion == 1" class="mt-5">
          <b-button size="sm" variant="warning" class="mr-2" @click=DownloadFile()>Descargue su archivo aquí</b-button>
    </div>
   
    <div v-if="this.ConvenioPago == 'CNB' || this.ConvenioPago == 'CCO' || this.ConvenioPago == 'PAGO' " class="mt-5">
          <b-button size="sm" variant="warning" class="mr-2" @click=DownloadFile()>Descargue su archivo aquí</b-button>
    </div>

    {{this.ConvenioPago}}


  <br/>
  <br/>
  <br/>
  <br/>
  </div> 

</template>  


<script>

import axios from 'axios'
import TiposIdenti from "../Data/TiposId.js";
import Municipios from "../Data/Municipio.js";
import Perfiles from "../Data/Perfiles.js";
import Servicios from "../Data/Servicios.js";
import Cargos from "../Data/Cargos.js";
import CargosApoyo from "../Data/CargoApoyo.js";
import { validationMixin } from "vuelidate";
import auth from "@/auth";
import {  required,  minLength,  alphaNum,  maxLength,  alpha,  numeric,} from "vuelidate/lib/validators";
import download from 'downloadjs'



export default {
  mixins: [validationMixin],
  data() {
    return {
      idPersona:null,
      CantidadRegistros:0,
      ConvenioPago:null,
      NombreEntidad:'',
        //Datos de la respuesta de la transaccion
        CodTransaccion: null,
        DescripcionTransaccion: null,      
       //URLactual: window.location,
       handler: ePayco.checkout.configure({
        key: 'e380e55975399fc99bbb840df6e2311a',
        test: false
      }), 
      data:{
          //Parametros compra (obligatorio)
          name: "Consultoria THS",
          description: "Consultoria THS",
          invoice: "",
          currency: "cop",
          amount: "50000",
          tax_base: "0",
          tax: "0",
          country: "co",
          lang: "en",

          //Onpage="false" - Standard="true"
          external: "true",


          //Atributos opcionales
          extra1: "extra1",
          extra2: "extra2",
          extra3: "extra3",
          //confirmation: "http://localhost:8080/#/regparticipante",
          //response: "http://localhost:8080/#/regparticipante",
          confirmation: "https://www.reportafacilths.com/#/regparticipante",
          response: "https://www.reportafacilths.com/#/regparticipante",


          //Atributos cliente
          name_billing: "",
          address_billing: "",
          type_doc_billing: "",
          mobilephone_billing: "",
          number_doc_billing: "",

         //atributo deshabilitación metodo de pago
          //methodsDisable: ["TDC", "PSE","SP","CASH","DP"]
          methodsDisable: []

          },
      ref_payco:'',
      CatPersonasGrilla:null,
      PersonasEntidad:null,
      BandFormulario:null,
      FechaCorte:null,
      IdGrilla:null,
      fruits: ['apple', 'banana', 'orange'],
      fields: [{key:'id',label:'Id'},{key:'TipoRegistro',label:'Tipo Registro',sortable:true},{key:'TipoId', lable:'Tipo Id'}, {key:'NroId',label:'Nro Id'}, {key:'PrimerApellido', lable:'Primer Apellido'},{key:'SegundoApellido', lable:'Segundo Apellido'},{key:'PrimerNombre', lable:'Primer Nombre'},{key:'SegundoNombre', lable:'Segundo Nombre'}, {key:'Acciones_de_tabla', lable:'Acciones_de_tabla'}],
      //style
      freezeFirstColumn: false,
      scrollVertical: true,
      scrollHorizontal: true,
      syncHeaderScroll: true,
			syncFooterScroll: true,
      includeFooter: true,
      deadAreaColor: "white",
			maxRows: 100,
      //Fin Style
      TiposId: TiposIdenti,
      Municipios: Municipios,
      Perfil: Perfiles,
      Servicio: Servicios,
      Cargo: Cargos,
      CargoApoyo: CargosApoyo,
      SelectCargo:null,
      AreaCovid: [
        { value: null, text: "Seleccione una opción" },
        { value: "01", text: "01 - ÁREA COVID" },
        { value: "02", text: "02 - OTRA ÁREA" },
      ],
      Dedicacion: [
        { value: null, text: "Seleccione una opción" },
        { value: "01", text: "01 - Tiempo completo" },
        { value: "02", text: "02 - Tiempo parcial" },
        { value: "03", text: "03 - Ocasional" },
      ],
      Indicador: [
        { value: null, text: "Seleccione una opción" },
        { value: "I", text: "I - Insertar el registro al sistema" },
        { value: "A", text: "A - Actualizar la información del registro" },
        { value: "E", text: "E - Eliminar el registro reportado por error" },
      ],
      EsThs: [
        { value: null, text: "Seleccione una opción" },
        { value: false, text: "SI" },
        { value: true, text: "NO" },
      ],
      errors: [],
      perfil: null,
      CodEnti: null,
      form: {
        tipoid: null,
        nroid: null,
        codentidad: this.CodEnti,
        nomentidad: null,
        papellido: null,
        sapellido: null,
        pnombre: null,
        snombre: null,
        municipio: null,
        //perfil: null,
        areacovid: null,
        servicio: null,
        dedicacion: null,
        cargo: null,
        indactualizacion: null,
        //status: null,
        EsThs: null,
      },
    };
  },
  validations: {
    form: {
      nroid: {required,minLength: minLength(3),maxLength: maxLength(17),alphaNum},
      tipoid: { required },
       codentidad: {minLength: minLength(10), maxLength: maxLength(10),numeric}, 
      nomentidad: {required,minLength: minLength(3),maxLength: maxLength(100)},
      papellido: {required,minLength: minLength(3),maxLength: maxLength(60)},
      sapellido: { minLength: minLength(3), maxLength: maxLength(60), alpha },
      pnombre: {required, minLength: minLength(3), maxLength: maxLength(60)},
      snombre: { minLength: minLength(3), maxLength: maxLength(60) },
      municipio: { required },
     // perfil: { required },
      areacovid: { required },
      servicio: { required },
      dedicacion: { required },
      cargo: { required },
      indactualizacion: { required },
      /*     status:{
        required
    }, */
      EsThs: {
        required,
      },
    },
  },

   mounted(){
//     this.LlenarGrillaPersonas()
      //this.getPersonas();  
      this.getName();
      this.getConsultaTransaccion();
      this.getDatosEntidad();
      this.LlenarGrillaPersonasMethod() ;
  },  

  methods: {
    getName(){
      this.ref_payco = this.$route.query.ref_payco; 
      console.log("wwwwwwwwwwwwwwwwwwwwwwwww:",this.ref_payco);

    },

     EnviarPago(){
       this.handler.open(this.data)

     },

      DownloadFile(){

        // calculo de la fecha en formato yyyy-MM-dd
        let date = new Date()
        let day = date.getDate()
        let month = date.getMonth() + 1
        let year = date.getFullYear()
        let EntidadconDiez = this.userLogged.entidad.substring(0,10);
        this.CantidadRegistros = this.PersonasEntidad.filter((item) => item.CodigoEntidad == this.userLogged.entidad).length;

        if(month < 10){
          month = "0"+month
        }
        if(day < 10){
          day = "0"+day        
         }       
        this.FechaCorte = year +'-'+ month +'-'+ day 
        let FechaCorteSinGuion = year + month + day

        var RegControl = "1|PI|"+EntidadconDiez+"|"+this.FechaCorte+"|"+this.FechaCorte+"|"+this.PersonasEntidad.length+'\r\n'
        //this.PersonasEntidad[0].TipoRegistro+"|"+"1"+"|"+this.PersonasEntidad[0].CodigoEntidad+"|"+this.PersonasEntidad[0].TipoId+"|"+this.PersonasEntidad[0].NroId+"|"+this.PersonasEntidad[0].PrimerApellido+"|"+this.PersonasEntidad[0].SegundoApellido+"|"+this.PersonasEntidad[0].PrimerNombre+"|"+this.PersonasEntidad[0].SegundoNombre+"|"+this.PersonasEntidad[0].CodigoMunicipio+"|"+this.PersonasEntidad[0].CodigoPerfil
        //+"|"+this.PersonasEntidad[0].CodigoEntidad+"|"+this.PersonasEntidad[0].NombreEntidad+"|"+this.PersonasEntidad[0].CodigoServicio+"|"+this.PersonasEntidad[0].CodigoAreaCovid+"|"+this.PersonasEntidad[0].CodigoDedicacion+"|"+this.PersonasEntidad[0].CodigoCargo+"|"+this.PersonasEntidad[0].IndicadorActualizacion


        var DatosArchivo = [];
        let str ="";
        let SApellidoSinNull = "";
        let SNombreNull = "";
        DatosArchivo.push(RegControl);	
        var consecutivo = 1;
        let cant = this.CantidadRegistros;
      
        this.PersonasEntidad.filter((item) => item.CodigoEntidad == this.userLogged.entidad).forEach(function(a){
            if(a["SegundoApellido"] != null) SApellidoSinNull = a["SegundoApellido"]; else SApellidoSinNull = "";
            if(a["SegundoNombre"] != null) SNombreNull = a["SegundoNombre"]; else SNombreNull = "";
           
            if(consecutivo < cant)
            {
              if(a["TipoRegistro"] == '2')
              str=a["TipoRegistro"]+"|"+consecutivo+"|"+a["TipoId"]+"|"+a["NroId"]+"|"+a["PrimerApellido"]+"|"+SApellidoSinNull+"|"+a["PrimerNombre"]+"|"+SNombreNull+"|"+a["CodigoMunicipio"]+"|"+a["CodigoPerfil"]+"|"+a["CodigoEntidad"]+"|"+a["NombreEntidad"]+"|"+a["CodigoServicio"]+"|"+a["CodigoAreaCovid"]+"|"+a["CodigoDedicacion"]+"|"+a["CodigoCargo"]+"|"+a["IndicadorActualizacion"] +'\r\n';
              else
              str=a["TipoRegistro"]+"|"+consecutivo+"|"+a["TipoId"]+"|"+a["NroId"]+"|"+a["PrimerApellido"]+"|"+SApellidoSinNull+"|"+a["PrimerNombre"]+"|"+SNombreNull+"|"+a["CodigoMunicipio"]+"|"+a["CodigoCargo"]+"|"+a["CodigoEntidad"]+"|"+a["NombreEntidad"]+"|"+a["CodigoServicio"]+"|"+a["CodigoAreaCovid"]+"|"+a["CodigoDedicacion"]+"|"+a["IndicadorActualizacion"] +'\r\n';
            }else{
              if(a["TipoRegistro"] == '2')
              str=a["TipoRegistro"]+"|"+consecutivo+"|"+a["TipoId"]+"|"+a["NroId"]+"|"+a["PrimerApellido"]+"|"+SApellidoSinNull+"|"+a["PrimerNombre"]+"|"+SNombreNull+"|"+a["CodigoMunicipio"]+"|"+a["CodigoPerfil"]+"|"+a["CodigoEntidad"]+"|"+a["NombreEntidad"]+"|"+a["CodigoServicio"]+"|"+a["CodigoAreaCovid"]+"|"+a["CodigoDedicacion"]+"|"+a["CodigoCargo"]+"|"+a["IndicadorActualizacion"];
              else
              str=a["TipoRegistro"]+"|"+consecutivo+"|"+a["TipoId"]+"|"+a["NroId"]+"|"+a["PrimerApellido"]+"|"+SApellidoSinNull+"|"+a["PrimerNombre"]+"|"+SNombreNull+"|"+a["CodigoMunicipio"]+"|"+a["CodigoCargo"]+"|"+a["CodigoEntidad"]+"|"+a["NombreEntidad"]+"|"+a["CodigoServicio"]+"|"+a["CodigoAreaCovid"]+"|"+a["CodigoDedicacion"]+"|"+a["IndicadorActualizacion"];
            }
            DatosArchivo.push(str)
            consecutivo= consecutivo + 1;
        });

        var cadena = new String(DatosArchivo);
        download(cadena.replace(/,/g,""), "THS310COVI"+FechaCorteSinGuion+"PI"+"00"+EntidadconDiez+".txt", "text/plain");
      },

      SetBanderaFormulario(valor){
        this.BandFormulario = valor
      },

      //metodo no en uso
      getPersonas(){
        axios.get('https://www.reportafacilthsapi.xyz/talento-humanos?_sort=TipoRegistro').then (response =>{
        this.PersonasEntidad = response.data;
        this.CodEnti = this.userLogged.entidad;
             
      })
      .catch (e => console.log(e))
    },

    getDatosEntidad(){
        console.log("Hola getDatosEntidad",this.userLogged.entidad)
        axios.get('https://www.reportafacilthsapi.xyz/prestador/' + this.userLogged.entidad ).then (response =>{
        this.NombreEntidad = response.data.Descripcion;
        this.ConvenioPago = response.data.ConvenioPago;
        //console.log("getDatosEntidad:",response.data.ConvenioPago)       
      })
      .catch (e => console.log(e))
    },    

    getConsultaTransaccion(){
      console.log("hola getConsultaTransaccion2222")   
      axios.get('https://secure.epayco.co/validation/v1/reference/' + this.ref_payco).then (response =>{
        this.CodTransaccion= response.data.data.x_cod_respuesta;
        this.DescripcionTransaccion = response.data.data.x_response_reason_text;
        //console.log("esta es wicho:",this.CodTransaccion)

        if(this.CodTransaccion == 1){
              axios.get('https://www.reportafacilthsapi.xyz/prestador/' + this.userLogged.entidad).then (response =>{
                this.idPersona= response.data.id;
                const conveniopago = {
                      ConvenioPago: "PAGO"
                   }   
                    auth.updateEntidadPago(conveniopago,this.idPersona);
                    //this.ConvenioPago = 
                    //console.log("esta es la persona:",response.data.id)
              })
              .catch (e => console.log(e))         
        }
      })
      .catch (e => console.log(e))
    },


    async EliminarParticipante(id){
      if(confirm("¿Seguro que desea Eliminar?")){
             try {
              await auth.EliminarPersona(id);
              this.getPersonas(); 
              //this.$router.push("/regparticipante");
            } catch (error) {
              this.error = true;              
              console.log(error)
            }  
            //this.$router.push("/regparticipante")    
            //this.$forceUpdate();
      }else{
        return ;
      }
    },

    async EditarParticipante(Pid,PTipoRegistro,PTipoId,PNroId,PPrimerApellido,PSegundoApellido,PPrimerNombre,PSegundoNombre,PCodigoMunicipio,PCodigoPerfil,PCodigoEntidad,PNombreEntidad,PCodigoServicio,PCodigoAreaCovid,PCodigoDedicacion,PCodigoCargo,PIndicadorActualizacion,PFechaCorte,TipoForm){
    if(PTipoRegistro == 2){
      PTipoRegistro = true
    }else
    PTipoRegistro = true

    this.SetBanderaFormulario(TipoForm);

      
      //se cargan las cajas de texto con los valores correspondientes para dejar lista la edicion
      this.IdGrilla = Pid
      this.$v.form.EsThs.$model =  PTipoRegistro
      this.$v.form.tipoid.$model = PTipoId
      this.form.nroid=PNroId
      this.codentidad = PCodigoEntidad
      this.form.nomentidad = PNombreEntidad
      this.form.papellido= PPrimerApellido
      this.form.sapellido= PSegundoApellido
      this.form.pnombre=PPrimerNombre
      this.form.snombre=PSegundoNombre
      this.$v.form.municipio.$model = PCodigoMunicipio
      this.perfil = PCodigoPerfil
      this.$v.form.areacovid.$model = PCodigoAreaCovid
      this.$v.form.servicio.$model = PCodigoServicio
      this.$v.form.dedicacion.$model = PCodigoDedicacion
      this.$v.form.cargo.$model = PCodigoCargo
      this.form.indactualizacion = PIndicadorActualizacion

    },


      LlenarGrillaPersonasMethod() {  
       
        axios.get('https://www.reportafacilthsapi.xyz/talento-humanos?CodigoEntidad=' + this.userLogged.entidad).then (response =>{
        this.PersonasEntidad = response.data;
        this.CodEnti = this.userLogged.entidad; 
        return this.PersonasEntidad
        //console.log ("this.PersonasEntidad",this.PersonasEntidad)      
      })
      .catch (e => console.log(e))
    }, 


    validateState(name) {
      const { $dirty, $error } = this.$v.form[name];
      return $dirty ? !$error : null;
    },
    resetForm() {
      this.form = {
        tipoid: null,
        nroid: null,
        codentidad: null,
        nomentidad: null,
        papellido: null,
        sapellido: null,
        pnombre: null,
        snombre: null,
        municipio: null,
        //perfil: null,
        areacovid: null,
        servicio: null,
        dedicacion: null,
        cargo: null,
        indactualizacion: null,
        //status: null,
        EsThs: null,
        EsThsCampo:null
      };

      this.$nextTick(() => {
        this.$v.$reset();
      });
    },

    async onSubmit() {

      this.$v.form.$touch();
      if (this.$v.form.$anyError) {
        return;
      }
      else{
        if (this.$v.form.EsThs.$model) {            
            this.errors = [];
            if (this.perfil == null) { 
                        this.errors.push('El perfil profesional es obligatorio cuando se selecciona NO en personal de apoyo logístico.'); 
                        return;                       
                    }
        }
        //Cuando todas las validaciones pasan ok, se procede a almacenar el registro en la base de datos
        if (this.$v.form.EsThs.$model) {
            this.EsThsCampo = 2;
        }else{
            this.EsThsCampo = 3;
        }

        // calculo de la fecha en formato yyyy-MM-dd
        let date = new Date()
        let day = date.getDate()
        let month = date.getMonth() + 1
        let year = date.getFullYear()

        if(month < 10){
          month = "0"+month
        }
        if(day < 10){
          day = "0"+day        
         }
        this.FechaCorte = year + "-" + month +'-'+ day 

            try {
                    
                    const persona = {
                       TipoRegistro: this.EsThsCampo ,
                       TipoId: this.$v.form.tipoid.$model,
                       NroId:this.$v.form.nroid.$model,
                       PrimerApellido: this.$v.form.papellido.$model,
                       SegundoApellido: this.$v.form.sapellido.$model,
                       PrimerNombre: this.$v.form.pnombre.$model,
                       SegundoNombre: this.$v.form.snombre.$model,
                       CodigoMunicipio: this.$v.form.municipio.$model,
                       CodigoPerfil: this.perfil,
                       CodigoEntidad: this.userLogged.entidad,
                       NombreEntidad: this.$v.form.nomentidad.$model,
                       CodigoServicio: this.$v.form.servicio.$model,
                       CodigoAreaCovid: this.$v.form.areacovid.$model,
                       CodigoDedicacion: this.$v.form.dedicacion.$model,
                       CodigoCargo: this.$v.form.cargo.$model,
                       IndicadorActualizacion: this.$v.form.indactualizacion.$model,
                       FechaCorte:this.FechaCorte 
                   };                   
               
              //Dependiendo de la variable, se llama a editar o a insertar
              if (this.BandFormulario == 1){
                  await auth.setPersona(persona);
              } else{
                  await auth.updatePersona(persona,this.IdGrilla);
              } 

              this.getPersonas();
              //this.$router.push("/regparticipante");
            } catch (error) {
              this.error = true;
              console.log(error);
            }
      } 

 
    },
  },
  computed: {

     LlenarGrillaPersonas() {  
       
        axios.get('https://www.reportafacilthsapi.xyz/talento-humanos?CodigoEntidad=' + this.userLogged.entidad).then (response =>{
        this.PersonasEntidad = response.data;
        this.CodEnti = this.userLogged.entidad; 
        return this.PersonasEntidad
        console.log ("this.PersonasEntidad",this.PersonasEntidad)      
      })
      .catch (e => console.log(e))

      return this.PersonasEntidad
    },

    userLogged() {       
      return auth.getUserLogged();
    },

    LoadCargo(){

     // console.log("this.CargoApoyo",this.CargoApoyo)
      
      if (this.$v.form.EsThs.$model == false){       
        this.SelectCargo = this.CargoApoyo;
         //console.log("cargo THS:",this.SelectCargo )
        return this.SelectCargo;
      }
      else{        
        this.SelectCargo = this.Cargo;
        //console.log("cargo Apoyo:",this.SelectCargo)
        return this.SelectCargo;
      }
    }

  },


  props: {
    msg: String
  },
/*    watch: {
    "$route.query.URLactual" :{
      inmediate:true,
      handler(URLactual){
        console.log(`URLactual a cambiado desde componente detectada:${URLactual}`);
        if (URLactual == 1){            
            this.urlapp = 'https://secure.epayco.co/validation/v1/reference/' + URLactual;
            console.log("si es igual a 1:",this.urlapp );
        }
      }
    }

  }  */
};
</script>

<style>

table.scrolling .w3 {
	width: 4.5em;
	min-width: 4.5em;
	max-width: 4.5em;
  height:2em; 
}
table.scrolling .NroId {
	width: 6em;
	min-width: 6em;
	max-width: 6em;
}
table.scrolling .nombres {
	width: 9em;
	min-width: 9em;
	max-width: 9em;
}
table.scrolling .action {
	width: 12em;
	min-width: 12em;
	max-width: 12em;
}


table.scrolling .botones {
column-span: 3;
}
table.scrolling tfoot tr th {
	width: 130em;
	min-width: 130em;
	max-width: 130em;
}
table.freezeFirstColumn thead tr,
table.freezeFirstColumn tbody tr {
	display: block;
	width: min-content;
}
table.freezeFirstColumn thead td:first-child,
table.freezeFirstColumn tbody td:first-child,
table.freezeFirstColumn thead th:first-child,
table.freezeFirstColumn tbody th:first-child {
	position: sticky;
	position: -webkit-sticky;
	left: 0;
}
* {
	font-family: sans-serif;
}
.box {
	clear: both;
	padding: 0;
	min-height: 300px;
	height: 60vh;
  /* width: 100vh; */
	margin-left: auto;
	margin-right: auto;
	overflow: hidden;
}
@font-face {
	font-family: FontAwesome;
	src: url(https://cdnjs.cloudflare.com/ajax/libs/font-awesome/4.7.0/fonts/fontawesome-webfont.woff);
}
.fa {
	font-family: FontAwesome;
}
</style>