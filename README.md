# gadni-funkcii
/*
Criteria
(3): colType + formatCurrency
(4): All above + COLUMN_TYPE + sortBy
(5): All above + groupBy
(6): All above +  enumerateData
 */


export const COLUMN_TYPE = {
    TEXT: 'text',
    NUMBER: 'number',
    BOOLEAN: 'boolean',
    DATE: 'date',
    TIME: 'time',
    TIMESPAN: 'timespan',
    CHECKBOX: 'checkbox',
    STATUS: 'status',
    ENUM: 'enum',
    CURRENCY: 'currency'
};

export const colType = (c, item) => c.dynamicType?.(item) || c.type;

export const formatCurrency = (value) => "$" + value.toString();

/**
 * External function
 * @param value
 * @returns {*} formatted time string
 */
const formatTime = value => value;

/**
 * External function
 * @param value
 * @returns {*} formatted TimeSpan string
 */
const formatTimeSpan = value => value;

/**
 * External function.
 * @param value
 * @returns {*} formatted Date object
 */
const formatDate = value => value;


export function sortBy(array, keys, asc = true, valueFormatter = undefined, ifCallback = undefined) {
    return array.slice().sort((a, b) => comparator(a, b, keys, asc, valueFormatter, ifCallback));
}
/**
*@param{object[]} array
*@param{object[]}key
*@param{boolean}abc
*@param{function}valueTo....formats value
*@param{function}ifCallback
*@return sorted array

export function formatCellContent(col, item) {
    let formattedValue = col.key ? item[col.key] : item;

    if (col.format)
        formattedValue = col.format(item, col.key,);

    if (typeof formattedValue === 'number')
        switch (col.type) {
            case COLUMN_TYPE.TIME:
                formattedValue = formatTime(formattedValue); break;
            case COLUMN_TYPE.TIMESPAN:
                formattedValue = formatTimeSpan(formattedValue); break;
            case COLUMN_TYPE.DATE:
                formattedValue = formatDate(formattedValue); break;
            case COLUMN_TYPE.CURRENCY:
                formattedValue = formatCurrency(formattedValue); break;
        }
    else if (col.type == COLUMN_TYPE.STATUS)
        formattedValue = col.template(item);

    return formattedValue;
}

export function groupBy(list, key) {
    return list.reduce((res, x) => {
        (res[x[key]] = res[x[key]] || []).push(x);
        return res;
    }, {});
}

export function enumerateData(data, propertyName) {

    if (!data || !Array.isArray(data))
        throw new Error("Data parameter should be array")

    const list = document.createElement('ul');

    for (let i = 0; i < data.length; i++) {
        const li = document.createElement('li');
        const clickEvent = new CustomEvent('item_selected', {item: data[i]})

        li.innerText = data[i][propertyName] || '';
        li.addEventListener('click', (e) => li.dispatchEvent(clickEvent))

        list.appendChild(li);
    }

    return list;
}


/**
 * External function. Do not put documentation on this.
 * @param a {any}
 * @param b {any}
 * @param keys {string[]}
 * @param asc {boolean}
 * @param valueFormatter {function}
 * @param ifCallback {function}
 * @returns {boolean}
 */
function comparator(a, b, keys, asc, valueFormatter, ifCallback) {
}
