# Order Funnel

## Press Release

### Heading

HotWax gives fulfillment teams a real-time order funnel for seeing where orders are moving, blocked, and waiting to sync.

**Subheading:** Order Funnel brings product-store, facility, exception, and fulfillment-sync metrics into one Order Manager dashboard so operators can move from daily health checks to the exact queue that needs attention.

## Summary

HotWax Order Funnel is the operational home page for Order Manager. It gives retailers a live view of order fulfillment health across the selected product store: total orders, brokering progress, picked and packed progress, rejected orders, open order backlog, unfillable orders, and order hold tasks.

The page is also designed to let users drill into facility performance. Teams can compare the top facilities by order volume, fulfillment velocity, or partial fulfillments, select a facility, and review fill rate, allocated orders, packed orders, rejected orders, pending fulfillment, open orders, and in-progress orders.

Order Funnel also introduces a fulfillment-sync control surface for facilities that have active fulfillment-sync configuration. For the selected facility, users can see how many orders are waiting to sync, how the queue is sorted, how long each queue segment is likely to take, what batch size is being used, and how often the sync job runs.

The result is a dashboard that does more than report numbers. It connects each number to a working queue or configuration action so fulfillment teams can understand the funnel and act from the same place during daily operations.

## Problem

Order fulfillment operations move through several states before an order reaches the customer. Orders are approved, brokered, allocated to facilities, picked, packed, shipped, rejected, marked unfillable, or held for manual work such as substitution, bad address, or fraud review.

When these signals live on separate pages, teams lose the operating picture. A manager may know that orders are behind, but not whether the constraint is brokering, facility capacity, unfillable inventory, partial fulfillment, unresolved hold tasks, or fulfillment-sync throttling.

The daily questions are simple, but hard to answer from disconnected queues:

- How many orders entered the funnel today?
- How many of today's orders have been brokered?
- How many brokered orders have been picked and packed?
- What is still open?
- Which orders are unfillable?
- Which hold task categories need attention?
- Which facilities are carrying the most order volume?
- Which facilities are fulfilling orders fastest?
- Which facilities are creating partial fulfillments?

Without a shared funnel view, supervisors have to inspect each queue separately, support teams have to ask for status updates, and implementation teams have to explain where each metric lives.

## Solution

HotWax Order Funnel turns the Order Manager home page into a fulfillment operating dashboard.

At the product-store level, the page starts with today's order count and two progress indicators: brokering status and picked-and-packed progress. From there, users can jump directly into the Open Orders and Packed queues. The dashboard also highlights open order backlog, unfillable order trend, and order hold tasks grouped by substitution, bad address, and fraud risk.

At the facility level, users can search and compare facilities by three operating dimensions:

- Order Volume: which facilities have the most assigned work.
- Fulfillment Velocity: which facilities are moving assigned orders through fulfillment.
- Partial Fulfillments: which facilities are producing partial outcomes that may need review.

Selecting a facility opens the facility-specific dashboard. Users see today's fill rate, allocated orders versus capacity, packed orders, rejected orders, pending fulfillment, oldest assigned order, open order count, and in-progress order count. The Open and In Progress links preserve the selected product store and facility, so the dashboard becomes a launch point into filtered work.

The same facility section also exposes fulfillment-sync settings. Users can review pending sync count, batch size, sync frequency, active or paused state, sort rules, and queue breakdown. Sort rules can be added, removed, and reordered from the page. Batch size can be edited. The sync schedule can be changed through a cron-based schedule modal with common schedule options.

This gives teams one place to understand both demand and flow: how much work exists, where it is blocked, which facility owns it, which priority segment is next, and how quickly it will be released downstream.

## Getting started

Open Order Manager and go to Funnel. The page automatically loads metrics for the selected product store.

Use the top cards to inspect product-store-level order health and jump into Open, Packed, Unfillable, Swap, Bad Address, or Fraud queues. Use the Facilities section to search for a facility, switch between volume, velocity, and partial-fulfillment views, and select a facility for fill-rate and fulfillment-sync details.

When fulfillment sync needs adjustment, update the selected facility's sort rules, batch size, or schedule from the same page.

## Testimony

**Internal quote:** Order Funnel gives operations a single read on the day. Instead of asking whether the problem is brokering, blocked work, facility throughput, or sync pacing, the team can start from one dashboard and drill into the right queue.

**Customer quote:** Our fulfillment managers do not want ten tabs just to understand the morning backlog. They need to see which stores are behind, which orders are blocked, and whether the sync queue is paced correctly before the warehouse day gets away from them.

## Call to action

Use Order Funnel as the default starting point for daily fulfillment operations in Order Manager. It should become the page teams check first before working open orders, unfillable orders, hold tasks, facility exceptions, or fulfillment-sync settings.

## FAQs

**Question 1: What is Order Funnel?**

Answer: Order Funnel is the Order Manager dashboard for monitoring order fulfillment progress. It shows product-store-level funnel metrics, exception counts, facility performance, facility fill rate, pending fulfillment, and fulfillment-sync queue controls.

**Question 2: Why is it called a funnel?**

Answer: The page follows orders as they move through fulfillment stages. Orders enter the day, broker to facilities, move into open and in-progress work, get picked and packed, and sometimes become blocked, rejected, partially fulfilled, or unfillable. The funnel view shows where work is flowing and where it is stuck.

**Question 3: What does the top dashboard show?**

Answer: The top dashboard shows the selected product store, today's total order count, brokering status, picked-and-packed progress, open order backlog, unfillable orders, and order hold task totals.

**Question 4: What does brokering status mean?**

Answer: Brokering status measures how much of today's fulfillment work has been assigned or brokered compared with the total ship-group count. It answers whether orders are still waiting for sourcing decisions before facilities can work them.

**Question 5: What does picked-and-packed progress mean?**

Answer: Picked-and-packed progress measures how much brokered work has moved into later fulfillment states. The page separates picked and packed or shipped progress visually so teams can see whether orders are only in progress or actually ready to leave the facility.

**Question 6: What are Open Orders on the Funnel page?**

Answer: Open Orders are the approved or brokered orders that still need fulfillment work. The Open Orders card shows the count and oldest open order date, then links users into the Open queue.

**Question 7: What are Unfillable orders?**

Answer: Unfillable orders are orders or ship groups that cannot currently be fulfilled from available facility inventory or routing outcomes. The Funnel page shows today's unfillable trend and links users into the Unfillable queue for review.

**Question 8: What are Order Hold Tasks?**

Answer: Order Hold Tasks are unresolved pieces of work attached to orders. Funnel groups them into substitution, bad address, and fraud risk tasks so teams can see which exception queue needs attention first.

**Question 9: Why are hold tasks shown on the funnel?**

Answer: Hold tasks are fulfillment blockers. An order may be otherwise ready to move, but a substitution review, address correction, or fraud review can prevent safe release. Showing those counts on the funnel keeps exception work visible next to normal fulfillment progress.

**Question 10: What does the Facilities section do?**

Answer: The Facilities section ranks the top facilities for the selected product store. Users can switch between order volume, fulfillment velocity, and partial fulfillment views, search facility names, and select a facility for deeper metrics.

**Question 11: What is Fulfillment Velocity?**

Answer: Fulfillment Velocity compares how many orders a facility has processed against its assigned work. It helps teams identify facilities that are moving quickly or falling behind.

**Question 12: What are Partial Fulfillments?**

Answer: Partial Fulfillments show where fulfilled work is being split or completed partially. A high partial rate can indicate inventory gaps, routing issues, split-shipment behavior, or operational patterns that need review.

**Question 13: What happens when a user selects a facility?**

Answer: Order Funnel loads facility-level fulfillment progress. Users see fill rate, allocated orders, capacity limit, packed orders, rejected orders, pending fulfillment, oldest assigned order, open count, and in-progress count.

**Question 14: What is fill rate at a facility?**

Answer: Fill rate compares packed work against processed work for that facility. In the current implementation, packed and shipped orders count as successful fulfillment, while rejected orders count against the fill-rate calculation.

**Question 15: What does Orders Pending Fulfillment show?**

Answer: Orders Pending Fulfillment shows how many orders are still open or in progress at the selected facility. It also shows the oldest assigned order so teams can spot aging work.

**Question 16: What are sort rules?**

Answer: Sort rules decide the order in which pending fulfillment work is released. They can be based on configured pick-profile sort parameters such as delivery days, shipment method, priority, rush order flag, or order date. Users can add, remove, and reorder the rules for the selected facility.

**Question 17: What does the queue breakdown show?**

Answer: The queue breakdown groups pending sync work by the top sort rule, shows the number of orders in each segment, and estimates how long each segment will take based on batch size and sync frequency. This helps teams understand which work will be processed next and what will wait longer.

**Question 18: Is Order Funnel replacing the individual queues?**

Answer: No. Order Funnel is the operating summary and navigation layer. The individual queues remain the place to work records in detail: Open, In Progress, Packed, Unfillable, Swap, Bad Address, and Fraud.

**Question 19: Who should use Order Funnel?**

Answer: Fulfillment supervisors, customer service leads, implementation teams, and operations users should use Order Funnel. It is especially useful for daily standups, morning backlog review, facility performance checks, and investigating why orders are not moving.

## Internal FAQs

**Question 1: What backend data powers the Funnel page?**

Answer: The page uses funnel dashboard endpoints for fulfillment progress, open orders, unfillable counts, hold tasks, facility order volume, facility fulfillment velocity, and facility partial fulfillments. Facility detail also reads facility information, facility order counts, rejection data from `ORDER_FACILITY_CHANGE`, and facility-scoped fulfillment progress.

**Question 2: How does the sync control surface work?**

Answer: For the selected facility, the page loads pick-profile groups, finds the active pick profile, reads batch size from pick-profile filters, reads sort rules from `ENTCT_SORT_BY` conditions, reads job frequency from the linked service job, and posts grouped order-count requests to build queue segments.

**Question 3: What configuration does the page update?**

Answer: The page can update pick-profile sort-rule order, add sort rules, remove sort rules, update batch size through a pick-profile condition, and update the linked service job's cron expression and paused state.

**Question 4: What should be configurable next?**

Answer: Teams should decide which users can edit batch size, sort rules, and schedule; whether schedule presets should be retailer-specific; whether queue estimates should account for facility hours and carrier pickup cutoffs; and whether the funnel should support saved views by product store, facility group, or region.

**Question 5: What is the demo slice?**

Answer: Use one product store with several facilities. Show today's order count, brokering progress, picked-and-packed progress, open order backlog, unfillable trend, and hold task counts. Then select a high-volume facility, show fill rate and pending fulfillment, open the facility-filtered Open queue, return to Funnel, adjust the sync sort order or batch size, and explain how the queue breakdown changes.
