
1、原始复杂取json转对象
```
        List<EnumType> listEnumTpye = new ArrayList<>();
        String channelEnumType = mtConfigClient.getValue("channelEnumType");
        JSONObject jsonObject = JSONObject.parseObject(channelEnumType);
        for(Map.Entry<String, Object> entry : jsonObject.entrySet()){
            EnumType enumType = new EnumType();
            JSONObject jsonObject1 = JSONObject.parseObject(JSONObject.toJSONString(entry.getValue()));
            enumType.setEnumTypeId(jsonObject1.getString("enumTypeId"));
            enumType.setEnumTypeName(jsonObject1.getString("enumTypeName"));
            List<Map<Object,Object>> listObjectSec = JSONArray.parseObject(jsonObject1.getString("enumList"),List.class);
            List<Item> items = new ArrayList<>();
            for(int i = 0; i<listObjectSec.size(); i++){
                items.add(new Item(listObjectSec.get(i).get("itemId"), String.valueOf(listObjectSec.get(i).get("itemName"))));
            }
            enumType.setEnumList(items);
            listEnumTpye.add(enumType);
        }
```
2、对象直接转换
```
        String channelEnumType = mtConfigClient.getValue("channelEnumType");
        List<EnumType> listEnumTpye = JSON.parseObject(channelEnumType, new TypeReference<List<EnumType>>() {
        });
```
形式不一样时用@JSONField
