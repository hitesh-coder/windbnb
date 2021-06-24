<template>
    <div>
        <div class="header">
            <div class="logo">
                <img src="../../assets/logo.svg" alt="" />
            </div>
            <div class="searchBox">
                <div class="locationDisplay" @click="displayMenu">
                    <span v-if="location != ''">{{ location }}, </span>
                    <span>Finland</span>
                </div>
                <div class="guestDisplay" @click="displayMenu">
                    <span v-if="noGuest == 0">Add Guests</span>
                    <span v-else>{{ noGuest }} Guests</span>
                </div>
                <div class="searchIcon" @click="displayMenu">
                    <i class="material-icons" style="color: #eb5757">search</i>
                </div>
            </div>
        </div>
        <div class="searchMenu" v-if="showMenu">
            <div class="locationColumn">
                <div class="locationInputHolder" v-on:click="isActive = true">
                    <span>Location</span>
                    <input
                        type="text"
                        name="location"
                        id="location"
                        v-model="location"
                        placeholder="Location"
                        class="locationInput"
                        :class="{ active: isActive }"
                        disabled
                    />
                </div>
                <div v-if="isActive" class="locationDropDownHolder">
                    <div
                        v-for="item in locations"
                        :key="item"
                        class="locationDropDown"
                    >
                        <span
                            v-on:click="changeLocation(item)"
                            class="particularLocation"
                            ><i class="material-icons" style="color: #eb5757"
                                >place</i
                            >
                            <p>{{ item }},Finland</p></span
                        >
                    </div>
                </div>
            </div>
            <div class="guestColumn">
                <div class="guestInputHolder" v-on:click="isActive = false">
                    <span>Guests</span>
                    <input
                        type="number"
                        v-model="noGuest"
                        class="guestInput"
                        :class="{ active: !isActive }"
                        disabled
                    />
                </div>
                <div v-if="!isActive" class="guestDropDown">
                    <div class="adults">
                        <h2>Adults</h2>
                        <h3>Ages 13 or above</h3>
                        <h4>
                            <span v-on:click="minusAdultGuest">-</span>
                            <p>{{ adultGuest }}</p>
                            <span v-on:click="plusAdultGuest">+</span>
                        </h4>
                    </div>
                    <div class="children">
                        <h2>Children</h2>
                        <h3>Ages 2-12</h3>
                        <h4>
                            <span v-on:click="minusChildrenGuest">-</span>
                            <p>{{ childrenGuest }}</p>
                            <span v-on:click="plusChildrenGuest">+</span>
                        </h4>
                    </div>
                </div>
            </div>
            <div class="closeSearchIcon" @click="displayMenu">
                <div>
                    <i class="material-icons" style="color: white">search</i>
                    <p>Search</p>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    name: "search",
    data() {
        return {
            location: "",
            locations: ["Helsinki", "Turku", "Oulu", "Vaasa"],
            noGuest: 0,
            adultGuest: 0,
            childrenGuest: 0,
            isActive: true,
            Guests: "Guests",
            showMenu: false,
        };
    },
    methods: {
        changeLocation(value) {
            this.location = value;
            this.$emit("locationRecive", this.location);
        },
        changeNoGuest() {
            this.$emit("noGuestRecive", this.noGuest);
        },
        guestCount() {
            this.noGuest = this.adultGuest + this.childrenGuest;
            this.changeNoGuest();
        },
        minusAdultGuest() {
            if (this.adultGuest > 0) {
                --this.adultGuest;
            }
            this.guestCount();
        },
        plusAdultGuest() {
            ++this.adultGuest;
            this.guestCount();
        },
        plusChildrenGuest() {
            ++this.childrenGuest;
            this.guestCount();
        },
        minusChildrenGuest() {
            if (this.childrenGuest > 0) {
                --this.childrenGuest;
            }
            this.guestCount();
        },
        displayMenu() {
            this.showMenu = !this.showMenu;
        },
    },
};
</script>

<style lang="scss" scoped>
* {
    font-family: Mulish;
}

.blur {
    background: rgba(0, 0, 0, 0.3);
}

.logo {
    margin: 0.7rem 0;
    position: absolute;
}
.searchBox {
    display: flex;
    flex-direction: row;
    justify-content: flex-end;
    // align-items: center;

    .locationDisplay {
        border-top-left-radius: 1rem;
        border-bottom-left-radius: 1rem;
    }
    .searchIcon {
        border-top-right-radius: 1rem;
        border-bottom-right-radius: 1rem;
    }

    .locationDisplay,
    .guestDisplay,
    .searchIcon {
        position: relative;
        right: 0%;
        padding: 0.5rem 1rem;
        border: 0.1px solid rgba(153, 153, 153, 0.1);
        box-shadow: 0px 0.5px 1px rgba(56, 56, 56, 0.301);
        cursor: pointer;

        span {
            font-style: normal;
            font-weight: normal;
            font-size: 14px;
            line-height: 18px;

            color: #333333;
        }
    }
}
.searchMenu {
    position: fixed;
    top: 3rem;
    z-index: 10;
    background: white;
    width: 80vw;
    padding: 3rem;
    border-radius: 1rem;
    box-shadow: 0px 1px 10px rgba(83, 83, 83, 0.472);
    display: flex;
    flex-direction: row;

    .active {
        border: 1px solid black !important;
    }

    .locationInputHolder,
    .guestInputHolder {
        position: relative;
        display: inline-block;
        box-shadow: 0px 0px 1px rgba(0, 0, 0, 0.4);
        margin-bottom: 0.5rem;

        span {
            position: absolute;
            left: 0.8rem;
            top: 5px;

            font-style: normal;
            font-weight: 800;
            font-size: 9px;
            line-height: 11px;
            color: #333333;
        }
        .locationInput,
        .guestInput {
            padding: 0.7rem;
            padding-top: 1rem;
            border-radius: 1rem;
            background: white;
            width: 25vw;
            border: none;

            font-style: normal;
            font-weight: normal;
            font-size: 14px;
            line-height: 18px;
            color: #333333;
        }
    }

    .closeSearchIcon {
        position: relative;
        box-shadow: 0px 0px 1px rgba(0, 0, 0, 0.4);
        height: fit-content;
        width: 15vw;
        display: flex;
        justify-content: center;

        div {
            display: flex;
            flex-direction: row;
            align-items: center;
            width: fit-content;
            background: #eb5757;

            border-radius: 1rem;
            padding: 0.7rem 1rem;
            cursor: pointer;

            p {
                font-style: normal;
                font-weight: normal;
                font-size: 14px;
                line-height: 18px;
                color: white;
            }
        }
    }

    .locationDropDown {
        color: #4f4f4f;

        .particularLocation {
            display: inline-flex;
            flex-direction: row;
            align-items: center;
            margin-top: 0.8rem;
            cursor: pointer;
            &:hover {
                text-shadow: 0.3px 0.3px rgba(78, 78, 78, 0.5);
            }
        }

        p {
            display: inline-block;
            font-weight: normal;
            font-size: 14px;
            line-height: 18px;
            cursor: pointer;
        }
    }

    .guestDropDown {
        padding-top: 0.7rem;
        h2,
        h3 {
            font-style: normal;
            font-weight: bold;
            font-size: 14px;
            line-height: 18px;

            color: #333333;
        }
        h3 {
            color: rgba(160, 160, 160, 0.7);
            font-weight: normal;
            margin-bottom: 0.3rem;
        }
        h4 {
            display: flex;
            flex-direction: row;
            align-items: center;
            margin-bottom: 0.6rem;
            * {
                margin-right: 0.5rem;
            }
            span {
                padding: 0.03rem 0.2rem;
                border: 1px solid black;
                border-radius: 0.3rem;
                cursor: pointer;
            }
        }
    }
}

@media screen and (max-width: 1100px) {
    .searchMenu {
        width: 90vw;
        top: 2rem;
        .locationInputHolder,
        .guestInputHolder {
            .locationInput,
            .guestInput {
                width: 30vw;
            }
        }
    }
}

@media screen and (max-width: 770px) {
    .searchMenu {
        .closeSearchIcon {
            width: 20vw;
        }
    }
}

@media screen and (max-width: 430px) {
    .logo {
        position: static;
    }
    .searchMenu {
        display: flex;
        flex-direction: column;
        padding: 1.5rem;
        top: 1rem;

        .locationInputHolder,
        .guestInputHolder {
            border-radius: 1rem;
            width: 100%;

            .locationInput,
            .guestInput {
                width: 100%;
            }
        }

        .locationDropDownHolder,
        .guestDropDown {
            margin-bottom: 1rem;
        }

        .closeSearchIcon {
            margin-left: 50%;
            transform: translate(-50%, 0);
        }
    }
}
</style>