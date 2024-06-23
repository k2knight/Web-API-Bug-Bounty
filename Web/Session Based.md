# Session Based

### Session Fixation

**Scenario 1** : copy cookie before login --> paste in another browser --> login in 2nd browser --> refresh the 1st browser after logging in 2nd browser --> if we logged IN in 1st browser it is session fixation 


**Scenario 2** (indented): login --> copy cookie --> import cookie in 2nd browser --> if we logged IN in 1st browser it is session fixation


**Scenario 3** : login --> copy cookie --> logout --> import copied cookie to the browser --> if we logged IN in 1st browser it is session fixation

#### Session Transmission


Session ID in URL Vulnerability
