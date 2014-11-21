state-machine
=============

	var TileState = {
		PENDING: 'PENDING',
		STREAMING: 'STREAMING',
		STOPPED: 'STOPPED'
	};

	function StreamingToStreamingTransition() {}

	StreamingToStreamingTransition.prototype.startState = TileState.STREAMING;
	StreamingToStreamingTransition.prototype.endState = TileState.STREAMING;
	
	StreamingToStreamingTransition.prototype.transitionAction = function(tileModel) {
		console.log('transition action');
	};

	var streamingToStreamingTransition = new StreamingToStreamingTransition();

	function StateMachine(options) { // options { transitions: transitions, initialState: initialState }
		this._transitions = options.transitions;
	}

	StateMachine.prototype.triggerTransition = function (endTileState, model) {
		var transition;

		transition = _findMatchingTransition(model.currentState, endTileState);

		if(!transition) {
			throw 'invalid transition';
		}

		return transition.transitionAction(model);
	};

	StateMachine.prototype._findMatchingTransition = function(startTileState, endTileState) {
		return this._transitions.find(function(t) { return t.startState === model.currentState && t.endState === endTileState });
	};

	function TileModelStateful(tileStateMachine) {
	  this._tileStateMachine = tileStateMachine;
	}

	var stateMachine = new StateMachine({ transitions: [ streamingToStreamingTransition ]});
