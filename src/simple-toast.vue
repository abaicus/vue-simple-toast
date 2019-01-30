<template>
	<div class="toast-wrap">
		<div class="toast" :class="[fadeOutClass, { dismissible }]" :style="coreStyle">
			<i v-if="iconClass" class="toast-icon" :class="iconClass"></i>
			<div class="message">{{toastMessage}}</div>
			<span v-if="dismissible" class="dismiss" @click="dismiss">+</span>
		</div>
	</div>
</template>

<script>
  const DEFAULT_COLOR_SUCCESS = '#1AB394'
  const DEFAULT_COLOR_ERROR = '#ED5565'
  const DEFAULT_COLOR_WARNING = '#F8AC59'

  /* jshint esversion: 6 */
  export default {
    name: 'toast',
    props: {
      color: {
        type: [String, Object],
        validator (value) {
          return typeof value === 'object'
              ? (value.success || value.error || value.warning)
              : typeof value === 'string'
        }
      },
      message: {
        type: String,
        required: true
      },
      iconClass: {
        type: String,
      },
      type: {
        type: String,
		default: 'success',
        validator (value) {
          return ['success', 'error', 'warning'].includes(value)
        }
      },
      dismissible: {
        type: Boolean,
        default: true
      },
      autoDismiss: {
        type: Boolean,
        default: false
      }
    },
    computed: {
      colorSuccess () {
        let { color } = this
        if (typeof color !== 'object') {
          return color || DEFAULT_COLOR_SUCCESS
        }
        return color.success
            ? color.success
            : DEFAULT_COLOR_SUCCESS
      },
      colorWarning () {
        let { color } = this
        if (typeof color !== 'object') {
          return color || DEFAULT_COLOR_WARNING
        }
        return color.warning
            ? color.warning
            : DEFAULT_COLOR_WARNING
      },
      colorError () {
        let { color } = this
        if (typeof color !== 'object') {
          return color || DEFAULT_COLOR_ERROR
        }
        return color.error
            ? color.errpr
            : DEFAULT_COLOR_ERROR
      },
      coreStyle () {
        let colorMap = {
          'error': this.colorError,
          'success': this.colorSuccess,
          'warning': this.colorWarning
        }

        return {
          backgroundColor: colorMap[this.type]
        }
      },
    },
    data () {
      return {
        toastMessage: '',
        fadeOutClass: ''
      }
    },
    methods: {
      dismiss () {
        this.fadeOutClass = 'fade-out'
        setTimeout(() => {
          this.toastMessage = ''
        }, 600)
      }
    },
    mounted () {
      this.toastMessage = this.message
      if (!this.autoDismiss) return false
      setTimeout(() => {
        this.fadeOutClass = 'fade-out'
      }, 1700)
    }
  }
</script>

<style lang="scss" scoped>
	//<editor-fold desc="Heartpop animation">
	@mixin heartpop( $delay: .7s ) {
		-webkit-animation: heartpop 0.9s both;
		animation: heartpop 0.9s both;
		animation-delay: $delay;
		-webkit-animation-delay: $delay;
	}

	@-webkit-keyframes heartpop {
		0% {
			-webkit-transform: scale3d(1, 1, 1);
			transform: scale3d(1, 1, 1);
		}
		30% {
			-webkit-transform: scale3d(1.25, 0.75, 1);
			transform: scale3d(1.25, 0.75, 1);
		}
		40% {
			-webkit-transform: scale3d(0.75, 1.25, 1);
			transform: scale3d(0.75, 1.25, 1);
		}
		50% {
			-webkit-transform: scale3d(1.15, 0.85, 1);
			transform: scale3d(1.15, 0.85, 1);
		}
		65% {
			-webkit-transform: scale3d(0.95, 1.05, 1);
			transform: scale3d(0.95, 1.05, 1);
		}
		75% {
			-webkit-transform: scale3d(1.05, 0.95, 1);
			transform: scale3d(1.05, 0.95, 1);
		}
		100% {
			-webkit-transform: scale3d(1, 1, 1);
			transform: scale3d(1, 1, 1);
		}
	}

	@keyframes heartpop {
		0% {
			-webkit-transform: scale3d(1, 1, 1);
			transform: scale3d(1, 1, 1);
		}
		30% {
			-webkit-transform: scale3d(1.25, 0.75, 1);
			transform: scale3d(1.25, 0.75, 1);
		}
		40% {
			-webkit-transform: scale3d(0.75, 1.25, 1);
			transform: scale3d(0.75, 1.25, 1);
		}
		50% {
			-webkit-transform: scale3d(1.15, 0.85, 1);
			transform: scale3d(1.15, 0.85, 1);
		}
		65% {
			-webkit-transform: scale3d(0.95, 1.05, 1);
			transform: scale3d(0.95, 1.05, 1);
		}
		75% {
			-webkit-transform: scale3d(1.05, 0.95, 1);
			transform: scale3d(1.05, 0.95, 1);
		}
		100% {
			-webkit-transform: scale3d(1, 1, 1);
			transform: scale3d(1, 1, 1);
		}
	}

	//</editor-fold>

	//<editor-fold desc="Flip out animation">
	@mixin flip-out( $duration: .45s ) {
		-webkit-animation: flip-out $duration cubic-bezier(0.550, 0.085, 0.680, 0.530) both;
		animation: flip-out $duration cubic-bezier(0.550, 0.085, 0.680, 0.530) both;
	}

	@-webkit-keyframes flip-out {
		0% {
			-webkit-transform: rotateX(0);
			transform: rotateX(0);
			opacity: 1;
		}
		100% {
			-webkit-transform: rotateX(70deg);
			transform: rotateX(70deg);
			opacity: 0;
		}
	}

	@keyframes flip-out {
		0% {
			-webkit-transform: rotateX(0);
			transform: rotateX(0);
			opacity: 1;
		}
		100% {
			-webkit-transform: rotateX(70deg);
			transform: rotateX(70deg);
			opacity: 0;
		}
	}

	//</editor-fold

	//<editor-fold desc="Flip in animation">
	@mixin flip-in( $duration: .5s ) {
		-webkit-animation: flip-in $duration cubic-bezier(0.250, 0.460, 0.450, 0.940) both;
		animation: flip-in $duration cubic-bezier(0.250, 0.460, 0.450, 0.940) both;
	}

	@-webkit-keyframes flip-in {
		0% {
			-webkit-transform: rotateX(80deg);
			transform: rotateX(80deg);
			opacity: 0;
		}
		100% {
			-webkit-transform: rotateX(0);
			transform: rotateX(0);
			opacity: 1;
		}
	}

	@keyframes flip-in {
		0% {
			-webkit-transform: rotateX(80deg);
			transform: rotateX(80deg);
			opacity: 0;
		}
		100% {
			-webkit-transform: rotateX(0);
			transform: rotateX(0);
			opacity: 1;
		}
	}

	//</editor-fold>

	.toast-wrap {
		padding: 20px 0 0;
	}

	.toast {
		@include flip-in();
		border: 1px solid transparent;
		padding: 10px 15px;
		color: #fff;
		font-weight: 300;
		border-radius: 3px;
		display: flex;
		align-items: center;
		min-width: 250px;

		&.fade-out {
			@include flip-out(.4s);
		}

		.dismiss {
			background-color: rgba(0, 0, 0, .25);
			border-radius: 50%;
			cursor: pointer;
			transition: all .1s ease-out;
			margin-left: auto;
			display: block;
			padding: 0px 5px;
			font-family: sans-serif;
			font-weight: 500;
			transform: rotate( 45deg );
			font-size: 25px;
			line-height: 25px;
			&:hover {
				background-color: rgba(0, 0, 0, .5);
			}
		}
		.toast-icon {
			position: relative;
			margin-right: 5px;
			@include heartpop(.3s);
		}
		&.dismissible .message {
			margin-right: 15px;
		}
	}
</style>
