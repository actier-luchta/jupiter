<script setup lang="ts">
import {reactive} from "vue";
import CBox from "@/components/layout/CBox.vue";
import CAutocomplete from "@/components/form/CAutocomplete.vue";

interface 名簿型 {
    id: string
    姓: string
    名: string
}

const string: {
    入力値: string
    血液型: string[]
    ラベル: string
    スタイル: 'filled'|'outlined'|'underlined'
    placeholder: string
} = reactive({
    入力値: '',
    血液型: [
    'A型',
    'B型',
    'O型',
    'AB型',
    ],
    ラベル: 'ラベル',
    スタイル: 'filled',
    placeholder: '入力してください'
})

const object: {
    入力値: string
    名簿: 名簿型[]
    識別子: string
    ラベル: string
    スタイル: 'filled'|'outlined'|'underlined'
    placeholder: string
} = reactive({
    入力値: '',
    名簿: [
        {
            id: '1',
            姓: '田中',
            名: '太郎',
        },
        {
            id: '2',
            姓: '田中',
            名: '一郎',
        },
        {
            id: '3',
            姓: '鈴木',
            名: '花子',
        },
        {
            id: '4',
            姓: 'JOHNSON',
            名: 'MARY',
        },
    ],
    識別子: 'id',
    ラベル: 'ラベル',
    スタイル: 'filled',
    placeholder: '入力してください'
})

const clearable: {
    選択された値: string
    clearable: boolean
    スタイル: 'filled'|'outlined'|'underlined'
} = reactive({
    選択された値: '1',
    clearable: true,
    スタイル: 'filled'
})

const iserror: {
    選択された値: string
    isError: boolean
    スタイル: 'filled'|'outlined'|'underlined'
} = reactive({
    選択された値: '1',
    isError: true,
    スタイル: 'filled'
})

const disabled: {
    選択された値: string
    disabled: boolean
    スタイル: 'filled'|'outlined'|'underlined'
} = reactive({
    選択された値: '1',
    disabled: true,
    スタイル: 'filled'
})

const readonly: {
    選択された値: string
    readonly: boolean
    スタイル: 'filled'|'outlined'|'underlined'
} = reactive({
    選択された値: '1',
    readonly: true,
    スタイル: 'filled'
})

const 文字列配列の絞り込み = (item:string, searchText:string) => {
    const keyword = searchText.toUpperCase()
    return item.toUpperCase().indexOf(keyword) > -1
}
const オブジェクト配列の絞り込み = (item:名簿型, searchText:string) => {
    const keyword = searchText.toUpperCase()
    if(item.姓.toUpperCase().indexOf(keyword) > -1) return true
    return item.名.toUpperCase().indexOf(keyword) > -1
}
</script>

<template>
<Story
    title="Form / CAutocomplete"
    :layout="{ type: 'grid', width: 500 }"
>
<Variant title="文字列の配列の場合" auto-props-disabled>
        <c-box padding="large">
            <c-autocomplete
            v-model="string.入力値"
            :items="string.血液型"
            :filter="文字列配列の絞り込み"
            :label="string.ラベル"
            :placeholder="string.placeholder"
            :variant="string.スタイル"
            id="string"
            >
            </c-autocomplete>    
        </c-box>
        <template #controls>
            <HstText v-model="string.入力値" title="modelValue"/>
            <HstJson
                v-model="string.血液型"
                title="items"
            />
            <HstText v-model="string.ラベル" title="label"/>
            <HstSelect
            v-model="string.スタイル"
            title="variant"
            :options="[
                {value: 'filled', label: 'filled'},
                {value: 'outlined', label: 'outlined'},
                {value: 'underlined', label: 'underlined'},
            ]"
            />
            <HstText v-model="string.placeholder" title="placeholder"/>
        </template>
    </Variant>
    <Variant title="オブジェクト配列の場合" auto-props-disabled>
        <c-box padding="large">
            <c-autocomplete
            v-model="object.入力値"
            :items="object.名簿"
            :item-value="object.識別子"
            :filter="オブジェクト配列の絞り込み"
            :label="object.ラベル"
            :placeholder="object.placeholder"
            :variant="object.スタイル"
            id="object"
            >
                <template v-slot:selection="{item}">
                    {{ item.姓 }} {{ item.名 }}
                </template>
                <template v-slot:item="{item}">
                    {{ item.姓 }} {{ item.名 }}
                </template>
            </c-autocomplete>    
        </c-box>
        <template #controls>
            <HstText v-model="object.入力値" title="modelValue"/>
            <HstJson
                v-model="object.名簿"
                title="items"
            />
            <HstText v-model="object.識別子" title="itemValue"/>
            <HstText v-model="object.ラベル" title="label"/>
            <HstSelect
            v-model="object.スタイル"
            title="variant"
            :options="[
                {value: 'filled', label: 'filled'},
                {value: 'outlined', label: 'outlined'},
                {value: 'underlined', label: 'underlined'},
            ]"
            />
            <HstText v-model="object.placeholder" title="placeholder"/>
        </template>
    </Variant>
    <Variant title="clearable" auto-props-disabled>
        <c-box padding="large">
            <c-autocomplete
            v-model="clearable.選択された値"
            :items="object.名簿"
            item-value="id"
            :filter="オブジェクト配列の絞り込み"
            :variant="clearable.スタイル"
            placeholder="入力"
            :clearable="clearable.clearable"
            >
                <template v-slot:selection="{item}">
                    {{ item.姓 }} {{ item.名 }}
                </template>
                <template v-slot:item="{item}">
                    {{ item.姓 }} {{ item.名 }}
                </template>
            </c-autocomplete>
        </c-box>
        <template #controls>
            <HstCheckbox
                v-model="clearable.clearable"
                title="clearable"
            />
            <HstSelect
            v-model="clearable.スタイル"
            title="variant"
            :options="[
                {value: 'filled', label: 'filled'},
                {value: 'outlined', label: 'outlined'},
                {value: 'underlined', label: 'underlined'},
            ]"
            />
        </template>
    </Variant>
    <Variant title="非活性" auto-props-disabled>
        <c-box padding="large">
            <c-autocomplete
            v-model="disabled.選択された値"
            :items="object.名簿"
            item-value="id"
            :filter="オブジェクト配列の絞り込み"
            :variant="disabled.スタイル"
            placeholder="入力"
            :disabled="disabled.disabled"
            >
                <template v-slot:selection="{item}">
                    {{ item.姓 }} {{ item.名 }}
                </template>
                <template v-slot:item="{item}">
                    {{ item.姓 }} {{ item.名 }}
                </template>
            </c-autocomplete>
        </c-box>
        <template #controls>
            <HstCheckbox
                v-model="disabled.disabled"
                title="disabled"
            />
            <HstSelect
            v-model="disabled.スタイル"
            title="variant"
            :options="[
                {value: 'filled', label: 'filled'},
                {value: 'outlined', label: 'outlined'},
                {value: 'underlined', label: 'underlined'},
            ]"
            />
        </template>
    </Variant>
    <Variant title="読み取り専用" auto-props-disabled>
        <c-box padding="large">
            <c-autocomplete
            v-model="readonly.選択された値"
            :items="object.名簿"
            item-value="id"
            :filter="オブジェクト配列の絞り込み"
            :variant="readonly.スタイル"
            :readonly="readonly.readonly"
            >
                <template v-slot:selection="{item}">
                    {{ item.姓 }} {{ item.名 }}
                </template>
                <template v-slot:item="{item}">
                    {{ item.姓 }} {{ item.名 }}
                </template>
            </c-autocomplete>
        </c-box>
        <template #controls>
            <HstCheckbox
                v-model="readonly.readonly"
                title="readonly"
            />
            <HstSelect
            v-model="readonly.スタイル"
            title="variant"
            :options="[
                {value: 'filled', label: 'filled'},
                {value: 'outlined', label: 'outlined'},
                {value: 'underlined', label: 'underlined'},
            ]"
            />
        </template>
    </Variant>
    <Variant title="警告" auto-props-disabled>
        <c-box padding="large">
            <c-autocomplete
            v-model="iserror.選択された値"
            :items="object.名簿"
            item-value="id"
            :filter="オブジェクト配列の絞り込み"
            :variant="iserror.スタイル"
            placeholder="入力"
            :is-error="iserror.isError"
            >
                <template v-slot:selection="{item}">
                    {{ item.姓 }} {{ item.名 }}
                </template>
                <template v-slot:item="{item}">
                    {{ item.姓 }} {{ item.名 }}
                </template>
                <template v-slot:errorMessage>
                    名前を入力してください
                </template>
            </c-autocomplete>
        </c-box>
        <template #controls>
            <HstCheckbox
                v-model="iserror.isError"
                title="isError"
            />
            <HstSelect
            v-model="iserror.スタイル"
            title="variant"
            :options="[
                {value: 'filled', label: 'filled'},
                {value: 'outlined', label: 'outlined'},
                {value: 'underlined', label: 'underlined'},
            ]"
            />
        </template>
    </Variant>
</Story>
</template>

<docs lang="md">
# CAutocomplete
入力補完機能のついたフォームコンポーネントです。

## Props

| Name | Type | Default | Description |
| --- | --- | --- | --- |
| modelValue | any | null | コンポーネントのv-model値です |
| items | any[] | [] | オブジェクトの配列、または文字列の配列を指定できます。オブジェクトの配列の場合、itemValueを使用することで、キーを変更できます。 |
| itemValue | string | '' | itemsがオブジェクトの配列の場合、識別するためのキーを指定することができます |
| filter | (item: any, searchText: string) => boolean | undefined | 絞り込みを行うための関数を指定します |
| label | string | '' | ラベルに設定するテキストを指定します |
| variant | 'filled'/'outlined'/'underlined' | 'filled' | コンポーネントに独自のスタイルを指定します |
| readonly | boolean | false | 読み取り専用にする場合は指定します |
| isError | boolean | false | コンポーネントをエラー状態にする場合は指定します |
| clearable | boolean | false | 入力したテキストをクリアするボタンを追加する場合は指定します |

## Slots

| Name | Props (if scoped) | Description |
| --- | --- | --- |
| selection | item | 選択された値の表示方法をカスタムできます |
| item | item/index | ドロップダウンリストの各項目の表示方法をカスタムできます |
| empty |  | ドロップダウンリストに一件も表示されない時に使用します |
| errorMessage |  | エラーの時のメッセージを表示する時に使用します |

## Events

| Name | Parameters | Description |
| --- | --- | --- |
| update:modelValue | - | コンポーネントのv-modelが変更されたときに発行されるイベントです |
</docs>
