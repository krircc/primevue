<template>
    <div class="p-splitbutton p-buttonset p-component">
        <PVSButton type="button" class="p-splitbutton-defaultbutton" :icon="icon" :label="label" @click="onClick" :disabled="disabled" :tabindex="tabindex" />
        <PVSButton type="button" class="p-splitbutton-menubutton" icon="pi pi-chevron-down" @click="onDropdownButtonClick" :disabled="disabled"
            aria-haspopup="true" :aria-controls="ariaId + '_overlay'"/>
        <PVSMenu :id="ariaId + '_overlay'" ref="menu" :model="model" :popup="true" :autoZIndex="autoZIndex"
            :baseZIndex="baseZIndex" :appendTo="appendTo" />
    </div>
</template>

<script>
import Button from '../button/Button';
import Menu from '../menu/Menu';
import UniqueComponentId from '../utils/UniqueComponentId';

export default {
    props: {
        label: {
            type: String,
            default: null
        },
        icon: {
            type: String,
            default: null
        },
		model: {
            type: Array,
            default: null
        },
        disabled: {
            type: Boolean,
            default: false
        },
        tabindex: {
            type: String,
            default: null
        },
        autoZIndex: {
            type: Boolean,
            default: true
        },
        baseZIndex: {
            type: Number,
            default: 0
        },
        appendTo: {
            type: String,
            default: null
        }
    },
    methods: {
        onClick(event) {
            this.$emit('click', event);
        },
        onDropdownButtonClick() {
            this.$refs.menu.toggle({currentTarget: this.$el, relativeAlign: this.appendTo == null});
        }
    },
    computed: {
        ariaId() {
            return UniqueComponentId();
        }
    },
    components: {
        'PVSButton': Button,
        'PVSMenu': Menu
    }
}
</script>

<style scoped>
.p-splitbutton {
    display: inline-flex;
    position: relative;
}

.p-splitbutton-defaultbutton {
    flex: 1 1 auto;
}

.p-splitbutton-menubutton {
    display: flex;
    align-items: center;
    justify-content: center;
}

.p-splitbutton .p-button:focus {
    z-index: 1;
}

.p-splitbutton .p-menu {
    min-width: 100%;
}

.p-fluid .p-splitbutton  {
    display: flex;
}
</style>
