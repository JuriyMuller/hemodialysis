<template>
  <div>
    <div class="session">
      <h2 class="session_title title">Назначения сеанса гемодиализа</h2>
      <div class="device">
        <h2 class="device_title subtitle">Программа аппарата</h2>
        <span
          v-for="(tag, idx) of tags"
          @click="active = active === idx ? null : idx"
          :key="tag.id"
          :class="{
            active: active === idx,
            static: true,
          }"
        >
          {{ tag.name }}
        </span>
      </div>
      <div class="dialyzer">
        <h2 class="dialyzer_title subtitle">Диализатор</h2>
        <input
          class="dialyzer_input input"
          type="text"
          value="Спр.Диализаторы "
        />
        <span class="dialyzer_btn btn"> </span>
      </div>
      <div class="concentrator">
        <div class="concentrator_inner">
          <h2 class="concentrator_title subtitle">Программа аппарата</h2>
          <h2 class="concentrator_title subtitle">Объем л.</h2>
        </div>
        <input
          class="concentrator_input input"
          type="text"
          value="Спр.Диализаторы "
        />
        <span class="concentrator_btn btn"> </span>
        <input class="concentrator_input_liters" type="text" value="10 л." />
      </div>
      <div class="type_of_injection">
        <h2 class="type_of_injection__title subtitle">Тип инъекции</h2>
        <span
          v-for="(tag, idx) of injection"
          @click="
            (activeIdx = activeIdx === idx ? null : idx),
              addAttribute(activeIdx)
          "
          :key="tag.id"
          :class="{
            active: activeIdx === idx,
            static: true,
          }"
        >
          {{ tag.name }}
        </span>
        <div class="type_of_injection_inner">
          <div class="type_of_injection__needle">
            <input
              class="type_of_injection__needle_item medications_needle_input"
              type="text"
              value="Спр. 'Иглы'"
            />
            <span
              @click="medicationsNeedlePopUp"
              class="type_of_injection__needle_item btn medications_needle_btn"
            >
            </span>

            <input
              class="type_of_injection__needle_item directory_needle_input"
              type="text"
              value="Спр. 'Типы иглы'"
            />
            <span
              class="type_of_injection__needle_item btn directory_needle_btn"
            >
            </span>
          </div>
          <div class="type_of_injection__сatheter">
            <input
              class="type_of_injection__сatheter_item medications_сatheter_input"
              type="text"
              value="Спр. 'Катетер'"
            />
            <span
              class="type_of_injection__сatheter_item btn medications_сatheter_btn"
            >
            </span>

            <input
              class="type_of_injection__сatheter_item directory_сatheter_input"
              type="text"
              value="Спр. 'Типы Катетеров'"
            />
            <span
              class="type_of_injection__сatheter_item btn directory_сatheter_btn"
            >
            </span>
          </div>
        </div>
        <div class="needle_popup">
          <h2 class="needle_popup_title subtitle">Лекарственные препараты</h2>
          <span class="needle_popup_btn">Закрыть</span>
          <div class="serch_items">
            <input class="needle_popup_search" type="text" />
            <span class="needle_popup_search_btn"></span>
          </div>
          <div class="add_items">
            <input class="needle_popup_add" type="text" />
            <span class="needle_popup_add_btn"></span>
          </div>

          <ul>
            <li>
              <span class="needle_popup_delete"></span>
              <span class="needle_popup_select"></span>
            </li>
          </ul>
        </div>
      </div>
    </div>
  </div>
</template>
<script>
import { json } from "body-parser";

export default {
  data() {
    return {
      active: null,
      activeIdx: null,
      tags: [
        {
          id: 1,
          name: "hd",
        },
        {
          id: 2,
          name: "hdf",
        },
        {
          id: 3,
          name: "uf",
        },
      ],
      injection: [
        {
          id: 1,
          name: "Игла",
        },
        {
          id: 2,
          name: "Катетер",
        },
      ],
    };
  },
  methods: {
    addAttribute(activeIdx) {
      let needle = document.querySelector(
          ".type_of_injection__needle"
        ).childNodes,
        сatheter = document.querySelector(
          ".type_of_injection__сatheter"
        ).childNodes;

      needle.forEach((e) => {
        сatheter.forEach((elem) => {
          if (activeIdx === 0) {
            elem.setAttribute("disabled", "disabled");
            e.removeAttribute("disabled", "disabled");
          } else if (activeIdx === 1) {
            e.setAttribute("disabled", "disabled");
            elem.removeAttribute("disabled", "disabled");
          } else {
            e.setAttribute("disabled", "disabled");
            elem.setAttribute("disabled", "disabled");
          }
        });
      });
    },
    medicationsNeedlePopUp() {},
  },
  async mounted() {
    const resp = await fetch("./Needles.json");
    const result = json(resp);
    console.log(result);
  },
};
</script>
<style>
.title {
  margin-bottom: 30px;
  font-weight: 500;
}
.subtitle {
  font-size: 18px;
  font-weight: 500;
  margin-bottom: 20px;
  padding-left: 10px;
}
.month {
  color: rgb(132, 132, 255);
}
.static {
  text-transform: uppercase;
  border-radius: 5px;
  border: 1px solid rgb(167, 167, 167);
  color: rgb(167, 167, 167);
}
.static + .static {
  margin-left: 20px;
}
.active {
  border: 2px solid rgb(52, 202, 145);
  color: rgb(52, 202, 145);
}
.static {
  display: inline-block;
  padding: 10px 50px;
}
.device,
.dialyzer,
.concentrator,
.type-of-injection {
  margin-bottom: 40px;
}
.concentrator_title {
  display: inline-block;
}
.concentrator_title + .concentrator_title {
  margin-left: 80px;
}
.concentrator_input_liters {
  position: relative;
  margin: 0 10px;
  padding: 10px 10px;
  max-width: 90px;
  text-align: center;
  font-size: 18px;
}
.type_of_injection_inner {
  margin-top: 40px;
}
.type_of_injection__сatheter,
.type_of_injection__needle {
  margin-bottom: 40px;
}
.type_of_injection__needle_item,
.type_of_injection__сatheter_item {
  margin-right: 10px;
  padding: 10px 10px;
}
.medications_btn {
  margin-right: 10px;
}
.needle_popup_btn {
  display: inline-block;
  padding: 10px 20px;
  border: 1px solid rgb(167, 167, 167);
  border-radius: 5px;
  font-size: 14px;
}
.needle_popup {
  max-width: 400px;
  padding: 20px;
  border: 1px solid black;
}
.needle_popup_title {
  margin: 30px 0;
  font-weight: 700;
}
.serch_items,
.add_items {
  margin: 10px 0;
}
.needle_popup_search,
.needle_popup_add {
  width: 80%;
  padding: 8px;
}
</style>
