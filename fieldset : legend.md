## Textarea

##### 여러줄의 일반 텍스트 양식

- rows
- Placeholder

## fieldset , legend

##### 같은 목적의 양식을 그룹화 하여 제목을 지정

```
<form>
  <fieldset>
    <legend>Coffee Size</legend>
    <label>
        <input type="radio" name="size" value="tall" />
        Tall
    </label>
    <label>
        <input type="radio" name="size" value="grande" />
        Grande
    </label>
    <label>
        <input type="radio" name="size" value="venti" />
        Venti
    </label>
  </fieldset>
</form>
```

## select / datalist / optgroup / option

##### 옵션 ( option / optgroup ) 의 선택메뉴 ( select ) 나 자동완성 ( datalist ) 제공

```
<select>
  <optgroup label="Coffee">
    <option>Americano</option>
    <option>Caffe Mocha</option>
    <option label="Cappuccino" value="Cappuccino"></option>
  </optgroup>
  <optgroup label="Latte" disabled>
    <option>Caffe Latte</option>
    <option>Vanilla Latte</option>
  </optgroup>
  <optgroup label="Smoothie">
    <option>Plain</option>
    <option>Strawberry</option>
    <option>Banana</option>
    <option>Mango</option>
  </optgroup>
</select>
```

 

```
select { display: inline-block; }
datalist { display: none; }
optgroup, option { display: block; }
```

### `<select>`

###### 옵션을 선택하는 메뉴

- autocomple
- disabled
- form
- multiple : 다중 선택
- name
- size : 한번에 볼수 있는 행의 개수



### `<optgroup>`

- label : option part 구분시 제목



### `<option>`

###### 선택메뉴 `<select>` 나 자동완성 `<datalist>` 에서 사용될 옵션

- disabled
- label : 표시될 옵션의 제목
- selected
- Value : 양식으로 제출될 값



##### `<datalist>` 

###### `<input>` 에 미리 정의된 옵션을 지정하여 자동완성 기능을 제공하는데 사용

- `<input>` 의 list 속성 바인딩
- `<option>`ㅇㅡㄹ 포함하여 정의된 옵션을 지정

```
<input type="text" list="fruits">

<datalist id="fruits">
  <option>Apple</option>
  <option>Orange</option>
  <option>Banana</option>
  <option>Mango</option>
  <option>Fineapple</option>
</datalist>
```

