<template>
    <div class="child-card" :style="{ animationDelay: `${index * 0.1}s` }">
        <div class="card-header">
            <div class="avatar" :style="{ background: `linear-gradient(135deg,${color},${color}88)` }">
                {{ getAvatar(m.name) }}
            </div>
            <div class="header-info">
                <p class="name">{{ m.name }}</p>
                <div class="level-badge" v-if="m.level !== '-'"
                    :style="{ background: `${color}22`, borderColor: `${color}55` }">
                    <svg viewBox="0 0 24 24" fill="currentColor" style="width: 12px; height: 12px;">
                        <polygon
                            points="12 2 15.09 8.26 22 9.27 17 14.14 18.18 21.02 12 17.77 5.82 21.02 7 14.14 2 9.27 8.91 8.26 12 2" />
                    </svg>
                    <span :style="{ color: color }">{{ m.level }}</span>
                </div>
            </div>
        </div>

        <div class="schedule-info">
            <span class="days">📅 {{ m.days }}</span>
            <span class="time" dir="ltr">🕐 {{ m.time }}</span>
        </div>

        <div class="note-section" v-if="m.note">
            <div class="note-header">
                <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"
                    style="width: 14px; height: 14px;">
                    <path d="M14 2H6a2 2 0 0 0-2 2v16a2 2 0 0 0 2 2h12a2 2 0 0 0 2-2V8z" />
                    <polyline points="14 2 14 8 20 8" />
                    <line x1="16" y1="13" x2="8" y2="13" />
                    <line x1="16" y1="17" x2="8" y2="17" />
                </svg>
                <span class="note-title">ملاحظة الكابتن</span>
            </div>
            <p class="note-text">{{ m.note }}</p>
        </div>
    </div>
</template>

<script setup>
import { computed } from 'vue'

const props = defineProps({
    m: {
        type: Object,
        required: true
    },
    index: {
        type: Number,
        default: 0
    }
})

const levelColors = {
    "Level 1": "#10B981", "Level 2": "#10B981", "Level 3": "#3B82F6",
    "Level 4": "#3B82F6", "Level 5": "#3B82F6", "Level 6": "#8B5CF6",
    "Level 7": "#8B5CF6", "Level 8": "#F59E0B", "Level 9": "#F59E0B",
    "Level 10": "#F59E0B", "Level 11": "#EF4444", "Level 12": "#EF4444",
    "Level 13": "#EF4444", "Level 14": "#EC4899", "Level 15": "#EC4899",
    "Level 16": "#EC4899", "Level 17": "#06B6D4", "Level 18": "#06B6D4",
    "Level 19": "#06B6D4", "Level 20": "#D4AF37", "Level 21": "#D4AF37",
    "Level 22": "#D4AF37",
}

const color = computed(() => levelColors[props.m.level] || "#00b4d8")

const getAvatar = (name) => {
    return name?.trim()?.[0] || "؟"
}
</script>

<style scoped>
.child-card {
    background: rgba(255, 255, 255, 0.04);
    backdrop-filter: blur(10px);
    border-radius: 20px;
    border: 1px solid rgba(0, 180, 216, 0.18);
    padding: 18px 18px 14px;
    margin-bottom: 12px;
    box-shadow: 0 8px 32px rgba(0, 0, 0, 0.3);
    animation: slideUp 0.4s ease both;
}

@keyframes slideUp {
    from {
        opacity: 0;
        transform: translateY(18px);
    }

    to {
        opacity: 1;
        transform: translateY(0);
    }
}

.card-header {
    display: flex;
    align-items: center;
    gap: 12px;
    margin-bottom: 14px;
}

.avatar {
    width: 52px;
    height: 52px;
    border-radius: 50%;
    flex-shrink: 0;
    display: flex;
    align-items: center;
    justify-content: center;
    font-size: 20px;
    color: #fff;
    font-weight: 900;
    box-shadow: 0 4px 16px rgba(0, 180, 216, 0.33);
    border: 2.5px solid rgba(212, 175, 55, 0.3);
}

.header-info {
    flex: 1;
}

.name {
    margin: 0 0 6px;
    color: #fff;
    font-size: 16px;
    font-weight: 900;
    line-height: 1.3;
}

.level-badge {
    display: inline-flex;
    align-items: center;
    gap: 4px;
    border-radius: 20px;
    padding: 3px 11px;
    font-size: 12px;
    font-weight: 700;
    border: 1px solid;
}

.schedule-info {
    display: flex;
    align-items: center;
    justify-content: space-between;
    padding: 10px 13px;
    border-radius: 12px;
    background: rgba(0, 180, 216, 0.07);
    border: 1px solid rgba(0, 180, 216, 0.12);
    margin-bottom: 10px;
}

.days {
    background: linear-gradient(135deg, #D4AF37, #f0d060);
    -webkit-background-clip: text;
    background-clip: text;
    -webkit-text-fill-color: transparent;
    font-weight: 800;
    font-size: 14px;
}

.time {
    color: rgba(144, 224, 239, 0.85);
    font-size: 13px;
    font-weight: 600;
}

.note-section {
    margin-top: 10px;
    padding: 11px 13px;
    background: rgba(212, 175, 55, 0.07);
    border-radius: 12px;
    border: 1px solid rgba(212, 175, 55, 0.18);
}

.note-header {
    display: flex;
    align-items: center;
    gap: 7px;
    margin-bottom: 6px;
    color: #D4AF37;
    font-size: 12px;
    font-weight: 700;
}

.note-text {
    margin: 0;
    color: rgba(240, 224, 150, 0.82);
    font-size: 13px;
    line-height: 1.65;
    font-weight: 600;
}
</style>