Задание 1 – Создать объект counter всеми возможными способами;

    let counter = {}
    let counter = new Object([value])
    let counter = Object.create(null, {
        count: { writable: true, configurable: true, enumerable: true, value: 3 },
    })

    function createCounter(prop1, prop2) {

        this.prop1 = prop1
        this.prop2 = prop2
        this.prop3 = function () {
        console.log("I am function inside prop3")
        };
    }
    let counter = new createCounter("value for prop1", "value for prop2")

Задание 2 – Скопировать объект counter всеми возможными способами;

    let copy = {... source}

    let copy = JSON.parse(JSON.stringify(counter))

    let copy= Object.assign({}, counter)

    import _  from "lodash"
    let copy = _.cloneDeep(counter)

    let copy = structuredClone(counter);

    function copyFunction(obj) {

        let copy = {};

            for (let prop in obj) {
                if (obj.hasOwnProperty(prop)) {
                copy[prop] = obj[prop];
                }
        }

        return copy;
    }

    let copy = copyFunction(counter)

Задание 3 – Создать функцию makeCounter всеми описанными и возможными способами;

    function makeCounter(){}
    let makeCounter = function(){}
    let makeCounter = mkCntr(){}
    let makeCounter = () => {}
    let makeCounter = new Function(

        "initialValue",
        "let value = initialValue; return function(){value = ++value; console.log(value)}"

    );

    let makeCounter = (function () {

        //body

    })();

Бонус Задание 1 – Написать функцию глубокого сравнения двух объектов:

    const typeOf = (input) => {

        const rawObject = Object.prototype.toString.call(input).toLowerCase();
        const typeOfRegex = /\[object (.\*)]/g;
        const type = typeOfRegex.exec(rawObject)[1];
        return type;
    };

    const deepCompare = (source, target) => {
        if (typeOf(source) !== typeOf(target)) {
        return false;
        }

        if (typeOf(source) === "array") {
        if (source.length !== target.length) {
        return false;
        }
        return source.every((el, index) => deepCompare(el, target[index]));
        } else if (typeOf(source) === "object") {
        if (Object.keys(source).length !== Object.keys(target).length) {
        return false;
        }
        return Object.keys(source).every((key) =>
        deepCompare(source[key], target[key])
        );
        } else if (typeOf(source) === "date") {
        return source.getTime() === target.getTime();
        }

        return source === target;
    };

Бонус Задание 2 – Развернуть строку в обратном направлении при помощи методов массивов:

    function reverseStr(str) {

        return [...str].reverse().join("");

    }
