
<template>
    <span
        :class="[newType, size]"
        class="icon">
        <i :class="[newPack, newIcon, newCustomSize, customClass]"/>
        <fa-icon
            :icon="[newPack, newIcon]"
            :size="newCustomSize"
            :class="customClass"/>
    </span>
</template>
<script>

export default {
    name: 'BIcon',
    props: {
        type: { type: String, default: '' },
        pack: { type: String, default: 'fas' },
        icon: { type: String, default: '' },
        size: { type: String, default: '' },
        customSize: { type: String, default: '' },
        customClass: { type: [String, Array], default: '' },
        // This is used internally to show both MDI and FA icon
        both: { type: Boolean, default: false }
    },
    computed: {
    /**
             * Internal icon name based on the pack.
             * If pack is 'fa', gets the equivalent FA icon name of the MDI,
             * internal icons are always MDI.
             */
        newIcon() {
            if (!this.both) {
                if (this.newPack === 'mdi') {
                    return `${this.newPack}-${this.icon}`
                }
                return `${this.icon}`
            }
            return this.newPack === 'mdi'
        ? `${this.newPack}-${this.icon}`
        : `${this.getEquivalentIconOf(this.icon)}`
        },
        newPack() {
            return this.pack
        },
        newType() {
            if (!this.type) return ''
            const splitType = this.type.split('-')
            if (!splitType.length) return ''
            return `has-text-${splitType[1]}`
        },
        newCustomSize() {
            return this.customSize || this.customSizeByPack
        },
        customSizeByPack() {
            const defaultSize = this.newPack === 'mdi'
        ? 'mdi-24px'
        : 'fa-lg'
            const mediumSize = this.newPack === 'mdi'
        ? 'mdi-36px'
        : 'fa-2x'
            const largeSize = this.newPack === 'mdi'
        ? 'mdi-48px'
        : 'fa-3x'
            switch (this.size) {
                case 'is-small': return
                case 'is-medium': return mediumSize
                case 'is-large': return largeSize
                default: return defaultSize
            }
        }
    },
    methods: {
    /**
             * Equivalent FA icon name of the MDI.
             */
        getEquivalentIconOf(value) {
            switch (value) {
                case 'check': return 'check'
                case 'information': return 'info-circle'
                case 'check-circle': return 'check-circle'
                case 'alert': return 'exclamation-triangle'
                case 'alert-circle': return 'exclamation-circle'
                case 'arrow-up': return 'arrow-up'
                case 'chevron-right': return 'angle-right'
                case 'chevron-left': return 'angle-left'
                case 'chevron-down': return 'angle-down'
                case 'eye': return 'eye'
                case 'eye-off': return 'eye-slash'
                case 'menu-down': return 'caret-down'
                case 'menu-up': return 'caret-up'
                default: return value
            }
        }
    }
}
</script>
