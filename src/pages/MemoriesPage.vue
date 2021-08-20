<template>
    <ion-page>
        <ion-header>
            <ion-title>
                Mapa de transporte
            </ion-title>
        </ion-header>
        <ion-content>
            <h2>Activar Mapa
                <i class="fas fa-globe-americas"></i>
            </h2>
            <br>
            <hr>
            <br>
            <br>
            <ion-button @click=" updateMapa()" expand="block">Activar Mapa
                <i class="far fa-check-circle"></i>
            </ion-button>
            <br>
            <ion-button @click=" updateMapadesac()" expand="block">Desactivar Mapa
                <i class="fas fa-times"></i>
            </ion-button>
            

        </ion-content>
    </ion-page>
</template>

<script>
import {IonPage,IonHeader,IonTitle,IonContent,IonButton} from '@ionic/vue';
import '@/Firebase/init'
import firebase from 'firebase'
 const db=firebase.firestore()
  const colec=db.collection('mapa')
export default {
components:{
    IonPage,
    IonHeader,
    IonTitle,
    IonContent,
    IonButton
},
data() {
    return {
        mapas:[],
        activ:true,
        desac:false
    }
},
methods:{
    getMapa(){
        colec.onSnapshot((querySnapshot)=>{
         this.mapas=[] //Llenando la info
        querySnapshot.forEach((doc)=>{ //variable
          //console.log(doc.id,doc.data().nombre);
          this.mapas.push({
            id:doc.id,data:doc.data() //indico que agrego //id recoge y
          });
          //console.log(this.clientesA);
        })
      })
    },
    updateMapa(){
        colec.doc('Ijo8HMZRAOEuDiy3Wgue').set({
        activar:true,
        desactivar:false
       
      })
    },
    updateMapadesac(){
        colec.doc('Ijo8HMZRAOEuDiy3Wgue').set({
        activar:false,
        desactivar:true
       
      })
    }
},
mounted(){
    
}
}
</script>

<style >
ion-title{
    text-align: center;
}
h2{
    text-align: center;
}
ion-button{
    margin-top: 50px;
}
</style>