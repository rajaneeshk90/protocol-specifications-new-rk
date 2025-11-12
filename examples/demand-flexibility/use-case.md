# Demand Flexibility Use Case

## Overview
This use case describes the end-to-end journey of a consumer (residential, commercial, or aggregator) participating in a Demand Flexibility (DF) program with a utility provider.

---

## Step 1: Program Discovery

**Summary:** Consumers discover available DF programs using search APIs.

### Process:
- Consumer entity (household, business, or aggregator) sends search request to find available DF programs
- Search criteria include location, load capacity, participant type, and consumer segment
- Gateway broadcasts the search to all relevant utilities in the network
- Utilities respond with available programs matching the criteria and consumer characteristics

### Key Information Exchanged:
- Geographic location and coverage area
- Load capacity and flexibility capabilities (individual or aggregated)
- Consumer segment (residential, commercial, industrial)
- Program types and incentive structures tailored to consumer size
- Participation requirements, terms, and minimum commitment levels

---

## Step 2: Program Subscription

**Summary:** Consumer subscribes to selected DF program (directly or through aggregator).

### Process:
- Consumer entity selects a DF program from search results based on their capacity and preferences
- Submits subscription request with commitment details, capabilities, and participation constraints
- Utility reviews application, validates technical requirements, and confirms subscription
- Subscription becomes active with defined terms, conditions, and consumer-specific parameters

### Key Information Exchanged:
- Maximum load reduction capacity commitment (individual household or aggregated portfolio)
- Available flexibility timeframes, notice periods, and seasonal variations
- Incentive rates and payment terms appropriate to consumer segment
- Program duration, renewal options, and opt-out procedures
- Performance requirements, penalties, and consumer protection measures

---

## Step 3: DF Event Notification

**Summary:** The Moment of Truth - When the Grid Calls for Help

This step represents the convergence of sophisticated grid engineering and market dynamics. Unlike traditional power plant dispatch (where utilities own and control generation resources), DF events require negotiating with independent actors who have their own business priorities and technical constraints.

### The Grid Operator's Decision Matrix
When system stress is detected, grid operators must make rapid decisions balancing multiple factors:
- **Technical Requirements:** How much load reduction is needed, where on the grid, and for how long?
- **Economic Optimization:** Which participants can deliver flexibility most cost-effectively?
- **Reliability Assurance:** What's the confidence level that participants will actually perform?
- **System Impact:** How will reduced consumption affect voltage profiles and power flows?

### Process:
- **Grid Condition Assessment:** Operators analyze real-time data from thousands of sensors across the transmission and distribution network, identifying stress patterns that may lead to equipment overloads or frequency deviations
- **Optimization Algorithm Execution:** Advanced algorithms simultaneously solve for optimal participant selection, event timing, and incentive levels while respecting grid constraints and participant availability
- **Multi-Participant Coordination:** The system constructs event notifications for potentially hundreds of participants, each receiving customized requests based on their location, capacity, and contract terms
- **Real-time Validation:** Before sending notifications, the system validates that the proposed DF event will actually resolve the grid constraint without creating new problems elsewhere

### Key Information Exchanged:
- **Grid Context:** Current frequency (e.g., "49.8 Hz, declining"), transmission loading percentages, and projected stress duration
- **Locational Signals:** Specific grid areas where load reduction is most valuable (transmission constraints are highly location-dependent)
- **Economic Signals:** Real-time pricing that reflects both grid need and participant availability
- **Technical Requirements:** Precise timing (including required ramp rates), duration, and any operational constraints

---

## Step 4: Event Participation Confirmation

**Summary:** Commercial consumer confirms participation in DF event.

### Process:
- Commercial facility evaluates event requirements against operational constraints
- Determines available load reduction capacity for the event timeframe
- Commits to specific load reduction amount with confidence level
- Confirms participation with baseline and target consumption details

### Key Information Exchanged:
- Committed load reduction amount and confidence level
- Baseline consumption and target consumption during event
- Confirmation of participation timing and constraints
- Equipment and systems to be controlled during event
- Emergency override and safety procedures

---

## Step 5: Performance Verification

**Summary:** Utility verifies actual load reduction delivered during the DF event.

### Process:
- Utility collects real-time meter data during event period
- Compares actual consumption against calculated baseline
- Validates load reduction against commitment
- Assesses any deviations or operational constraints reported
- Calculates final performance metrics

### Key Information Exchanged:
- Actual consumption data with timestamps
- Baseline consumption for comparison
- Load reduction achieved (kW and duration)
- Performance percentage against commitment
- Any qualifying events or exceptions

---

## Step 6: Incentive Settlement

**Summary:** Utility processes incentive payments based on verified performance.

### Process:
- Utility calculates incentive amount based on verified performance
- Applies any adjustments for partial performance or exceptions
- Sends settlement notification with performance details
- Processes payment according to program terms
- Updates participant performance history

### Key Information Exchanged:
- Performance verification results
- Incentive calculation breakdown
- Payment amount and timing
- Settlement status and confirmation
- Updated performance metrics for future events
