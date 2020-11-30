# cascader
react/ant-design/cascader
#基于react+ant-design使用级联选择器
#项目要求：后端传来的数据信息，前端使用级联选择器完成渲染与选择
### 主要代码如下：
```javascript
    getoptions=(data)=>{
        const options=[];
        for(var key in data){
            const children= [];
            //获取option每个label的对应children
            if(typeof data[key].children === 'object' && Object.keys(data[key].children).length>0){
                data[key].children.forEach(item=>{
                    children.push({
                        value:item.value,
                        label:item.label,
                        value_type:item.value_type,
                    })
            })
        }
        options.push({
            value:data[key].value,
            label:data[key].label,
            children,
        })}
        return options;
    }
        
    onchange=(value,selectedValue)=>{
        console.log('changevalue',value);
        console.log('selectedvalue',selectedValue[1]);
        
    }

    render(){
        return(
           <Layout>
            <Row className='row-customconfig'>
                <Cascader className='custom-cascader'
                          size='large' 
                          options={this.getoptions(this.props.configform)}
                          expandTrigger='hover'
                          placeholder='请选择自定义Config'
                          onChange={this.onchange}
                          bordered={true}
                          />
            </Row>
```
###后端传来的config:即this.props.configform
```json
{"children":[{"label":"prefix","value":"'{}_'.format(date_string())","value_type":"NoneType"},
            {"label":"suffix","value":"'_t00'","value_type":"NoneType"},
            {"label":"model","value":"model","value_type":"NoneType"},
            {"label":"num_layers","value":"100","value_type":"int"},
            {"label":"layer_width","value":"50","value_type":"NoneType"},
            {"label":"bias_initializer","value":"-5.","value_type":"NoneType"},
            {"label":"optimizer","value":"tf.train.AdamOptimizer","value_type":"NoneType"},
            {"label":"learning_rate","value":"0.0002","value_type":"NoneType"},
            {"label":"mark","value":"'{}({}x{}-{})'.format(","value_type":"NoneType"},
            {"label":"input_shape","value":"[28,28,1]","value_type":"list"},
            {"label":"num_classes","value":"10","value_type":"int"}],
"label":"ModelConfig","value":"ModelConfig"},
{"children":[{"label":"val_decimals","value":"6","value_type":"int"},
            {"label":"train","value":"True","value_type":"bool"},
            {"label":"save_model","value":"False","value_type":"bool"},
            {"label":"overwrite","value":"True","value_type":"bool"},
            {"label":"save_model","value":"False","value_type":"bool"},
            {"label":"overwrite","value":"True","value_type":"bool"},
            {"label":"sample_num","value":"3","value_type":"int"},
            {"label":"val_batch_size","value":"1000","value_type":"int"},
            {"label":"evaluate_train_set","value":"True","value_type":"bool"},
            {"label":"evaluate_val_set","value":"True","value_type":"bool"},
            {"label":"evaluate_test_set","value":"True","value_type":"bool"}],
"label":"TrainConfig","value":"TrainConfig"},
{"children":[{"label":"gather_summ_name","value":"th.prefix+summ_name+th.suffix+'.sum'","value_type":"str"},
            {"label":"export_note","value":"False","value_type":"bool"},
            {"label":"gather_note","value":"True","value_type":"bool"},
            {"label":"export_tensors_upon_validation","value":"True","value_type":"bool"}],
 "label":"NoteConfig","value":"NoteConfig"},
{"children":[],"label":"RnnConfig","value":"RnnConfig"},
{"children":[],"label":"MonitorConfig","value":"MonitorConfig"},
{"children":[],"label":"CloudConfig","value":"CloudConfig"},
{"children":[],"label":"DataConfig","value":"DataConfig"},
{"children":[],"label":"AdvancedConfig","value":"AdvancedConfig"},
{"children":[{"label":"job_dir","value":"'/{:02d}_{}'.format(id,model_name)","value_type":"str"},
            {"label":"visible_gpu_id","value":"1","value_type":"NoneType"},
            {"label":"epoch","value":"400","value_type":"int"},
            {"label":"batch_size","value":"128","value_type":"int"},
            {"label":"validation_per_round","value":"2","value_type":"int"},
            {"label":"patience","value":"5","value_type":"int"},
            {"label":"early_stop","value":"False","value_type":"bool"},
            {"label":"validate_train_set","value":"True","value_type":"bool"},
            {"label":"data_dir","value":"from_root('task/00-MNIST/data/')","value_type":"str"},
            {"label":"job_dir","value":"from_root('task/00-MNIST')","value_type":"str"},
            {"label":"allow_growth","value":"False","value_type":"bool"},
            {"label":"gpu_memory_fraction","value":"0.30","value_type":"float"},
            {"label":"show_structure_detail","value":"True","value_type":"bool"},
            {"label":"keep_trainer_log","value":"True","value_type":"bool"},
            {"label":"warm_up_thres","value":"1","value_type":"int"},
            {"label":"early_stop","value":"True","value_type":"bool"},
            {"label":"patience","value":"6","value_type":"int"},
            {"label":"shuffle","value":"True","value_type":"bool"},
            {"label":"print_cycle","value":"5","value_type":"int"},
            {"label":"validation_per_round","value":"20","value_type":"int"}],
"label":"CommonConfig","value":"CommonConfig"}]
```

##实际效果：完成了初步渲染，也就是目录可以产生，但是会出现渲染混乱
![实际效果如下](https://github.com/rscv5/cascader/blob/main/%E9%97%AE%E9%A2%98%E6%8F%8F%E8%BF%B01.png)
