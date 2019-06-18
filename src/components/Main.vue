<template>
<div class="container pt-5" id="app">
        <div class="row md-3">
            <div class="col">
                <h2>Test Frontend Task</h2>
            </div>
        </div>
        <div class="row">
            <div class="col-md-4">
                <div class="form-group">
                    <label for="search">Country</label>
                    <input type="text" class="form-controli"  v-model="search"
                    id="search" placeholder=" Find country">
                </div>
                <hr>
                <ul class="list-group" >
                    <li class="list-group-item list-group-item-action"  @click="selectProxy(0)" :class="{'active': transparent===true}">Transparent</li>    
                    <li class="list-group-item list-group-item-action" @click="selectProxy(1)" :class="{'active': anonymous===true}">Anonymous</li>    
                    <li class="list-group-item list-group-item-action" @click="selectProxy(2)" :class="{'active': elite===true}">Elite</li>    
                    <li class="list-group-item list-group-item-action" @click="selectProxy(3)" :class="{'active': alive===true}" >Alive</li>    
                </ul>
            </div>
            <div class="col-md-8 pt-3">
                <div class="col-md-12">
                    <ul class="list-group">
                        <li v-for="(statu,index) of filteredProxyes" :key="index"  
                        class="list-group-item list-group-item-action">{{statu.created}} {{statu.id}} {{statu.modified}} {{statu.host}} 
                            {{statu.port}} {{statu.busy_until}} {{statu.last_check_time}} {{statu.proxy_type}} {{statu.port_response_time}} 
                            {{statu.chargeable}} {{statu.last_check_time}} {{statu.use_counter}} {{statu.protocol}} {{statu.source_of_statu}} 
                            <strong>Country  -{{statu.country}} </strong>  {{statu.alive}}</li>
                    </ul>
                </div>

            </div>
        </div>
</div>
</template>
<script src="https://unpkg.com/vue"></script>
<script src="https://unpkg.com/axios@0.19.0/dist/axios.min.js"></script>
<script>

export default {
 name:'app',
    created()
    {
        this.loadQuote();
    },
    data(){
        return{
        search:'',
        transparent:false,   
        anonymous:false,
        elite:false,
        alive:false,
        status:[],
        statu:status[0]
        }
    },
    computed:{
         filteredProxyes(){
            return this.someMeth(this.transparent,this.anonymous,this.elite,this.alive,this.status);
        }
    },
    methods:
    {
        async loadQuote(){
            await axios.get(`${'https://cors-anywhere.herokuapp.com/'}https://proxyfordevelopers.com/api/proxies/?format=json`)
            .then((response)=>{
                this.status=response.data;
            })
            .catch(function(error){
                this.status='Error '+error;
            })
        },
        selectProxy(property){
            if(property==0){
                this.transparent=!this.transparent
            }
            if(property==1){
                this.anonymous=!this.anonymous
            }
            if(property==2){
                this.elite=!this.elite
            }
            if(property==3){
                this.alive=!this.alive
            }
        },
        someMeth(cond1,cond2,cond3,cond4,prop1)
            {
            const cond13=cond1&&cond3;
            const cond12=cond1&&cond2;
            const cond23=cond2&&cond3;
            const cond123=cond1&&cond2&&cond3;
            if(cond4)
            {
                if(cond1)
                {
                    if(cond12)
                    {
                        if(cond123)
                        {
                             return prop1.filter(prop2=>{
                                return prop2.country.indexOf(this.search)>-1&&(prop2.alive==true)
                            })
                        }
                        else
                        {
                            return prop1.filter(prop2=>{
                                return prop2.country.indexOf(this.search)>-1&&(prop2.proxy_type==1||prop2.proxy_type==0)&&prop2.alive==true
                            })
                        }
                    }
                    if(cond13)
                    {
                        return prop1.filter(prop2=>{
                            return prop2.country.indexOf(this.search)>-1&&(prop2.proxy_type==2||prop2.proxy_type==0)&&prop2.alive==true
                        })
                    }
                    else
                    {
                        return prop1.filter(prop2=>{
                            return prop2.country.indexOf(this.search)>-1&&(prop2.proxy_type==0)&&prop2.alive==true
                        })
                    }
                }
                else if(cond2)
                {
                    if(cond23){
                        return prop1.filter(prop2=>{
                            return prop2.country.indexOf(this.search)>-1&&(prop2.proxy_type==2||prop2.proxy_type==1)&&prop2.alive==true
                        })
                    }
                    else{
                        return prop1.filter(prop2=>{
                            return prop2.country.indexOf(this.search)>-1&&(prop2.proxy_type==1)&&prop2.alive==true
                        })
                    }
                }
                else if(cond3)
                {
                    return prop1.filter(prop2=>{
                        return prop2.country.indexOf(this.search)>-1&&(prop2.proxy_type==2)&&prop2.alive==true
                    })
                }
                else
                {
                    return prop1.filter(prop2=>{
                        return prop2.country.indexOf(this.search)>-1&&prop2.alive==true
                    })
                }
            }
            else
            {
                if(cond1)
                {
                    if(cond12)
                    {
                        if(cond123)
                        {
                            return prop1.filter(prop2=>{
                                return prop2.country.indexOf(this.search)>-1
                            })
                        }
                        else
                        {
                            return prop1.filter(prop2=>{
                                return prop2.country.indexOf(this.search)>-1&&(prop2.proxy_type==1||prop2.proxy_type==0)
                            })
                        }
                    }
                    if(cond13)
                    {
                        return prop1.filter(prop2=>{
                            return prop2.country.indexOf(this.search)>-1&&(prop2.proxy_type==2||prop2.proxy_type==0)
                        })
                    }
                    else
                    {
                        return prop1.filter(prop2=>{
                            return prop2.country.indexOf(this.search)>-1&&(prop2.proxy_type==0)
                        })
                    }
                }
                else if(cond2)
                {
                    if(cond23)
                    {
                        return prop1.filter(prop2=>{
                            return prop2.country.indexOf(this.search)>-1&&(prop2.proxy_type==2||prop2.proxy_type==1)
                        })
                    }
                    else{
                        return prop1.filter(prop2=>{
                            return prop2.country.indexOf(this.search)>-1&&(prop2.proxy_type==1)
                        })
                    }
                }
                else if(cond3)
                {
                    return prop1.filter(prop2=>{
                        return prop2.country.indexOf(this.search)>-1&&(prop2.proxy_type==2)
                    })
                }
                else
                {
                    return prop1.filter(prop2=>{
                        return prop2.country.indexOf(this.search)>-1
                        })
                    }
                }
            }
        }
    }

</script>

