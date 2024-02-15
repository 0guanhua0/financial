Welcome, fellow members of the Turtle Pond.

This repo is going to hold all my spreadsheets (santized) for the financials around the VMW->AVGO acquisition.

By insistent recommendation of colleagues/friends that _they_ want to be able to pay something, I am going to see if I can enable Sponsor for the repo.
Don't feel obligated in any way to do so though - my goal is to provide as much support as possible for everyone else with the same set of concerns... and to get peer reviewed in turn to improve _my_ filing correctness!
For people that have insisted, I'm suggesting $3.80, $38, ... as an ironic echo of the _voluntary reorganization_ fee by eTrade, with the expectation of correct data out of the other side.

# Contents

The spreadsheet is exported from Google Sheets. I've tried opening it in Excel but it's not happy. If there are easy tweaks to make it comptiable that'll be my first change. Until then, import into Google Docs.

* [spreadsheet for ESPP & RSU basis and realized gain cacluations](https://github.com/hickeng/financial/raw/main/VMW%20to%20AVGO%20-%20ESPP%20&%20RSU%20worksheet.xlsx)


# On use of Issues

I'm opening issues to track questions and feature requests. Feel free to do the same.

If it's also applicable to me, I'll get to them (no latency guarantees).  If not it'll be best effort.


# References


## Form 8937
These forms detail tax handling for an event. This includes qualified/unqualified amounts, how to adjust cost-bases, how to calculate gain that must be realized, etc. These are pulled from the [Broadcom Invester Relations](https://investors.broadcom.com/financial-information/tax-information) site.

The acquisition form mostly uses non-imperative language, which leaves a lot of optionality for other treatments. My personal plan is to use the "generally ..." guidence absent a strong endorsement from a CPA for a different treatment being valid.

Links to the relevant Form 8937's:
* [Broadcom Acquisition](https://investors.broadcom.com/static-files/7720c4c1-c940-4d9d-800c-66819bfdc7a0)
* [Dell recapitalization 2021](https://investors.broadcom.com/static-files/7ba40d05-a5b8-454d-8140-7f9782069523) - applies if you received VMWs by virtue of owning Dell shares during the spin out.
* [Dell distribution 2021](https://investors.broadcom.com/static-files/c03396b2-538b-42c3-910c-dce218d5d9f1)
* [Dell distribution 2018](https://investors.broadcom.com/static-files/674c4fc3-6cc3-48cf-83b1-f6f6f3f75623)



### Pro-rata vs other allocation of cash/share split

> a shareholder ... is treated as having surrendered each share _for a pro rata portion of the stock and cash received_, based on the [fair market value](https://github.com/hickeng/financial/edit/main/README.md#on-fair-market-value) of such surrendered share, _unless the terms of the exchange provide otherwise and are economically reasonable_.

> If a holder of VMware Common Stock acquired different blocks of shares ... at different times or different prices, any gain or loss _may_ be determined separately for each block of shares ... . Any such holder should consult their tax advisor regarding the manner in which the Cash Consideration and Stock Consideration should be allocated among different blocks of shares of VMware Common Stock surrendered.

Per my reading, this explicitly states that we have the option to chose _not_ to use a pro-rata approach to calculating the cash/stock split. I've an [issue](https://github.com/hickeng/financial/issues/13) to collect data on _when_ we're allowed to make this choice.

The first quote is referencing the FMV of a VMW share at the time of acquisition. This should be fixed at $192.48 (?) based on knowledge at time of execution. I've an [issue](https://github.com/hickeng/financial/issues/14) to follow up on this:
* ratio of share/cash election
* VMW price ($142.50 from Merger agreement)
* AVGO FMV as of execution (2023-11-22 - [but when: after close? during trading?](https://github.com/hickeng/financial/issues/11))


### Realized gain calculation

> ... a holder ... who received a combination of ... Stock and cash ... will recognize gain (but not loss) for U.S. federal income tax purposes in an amount equal to the lesser of
> (1) the sum of the amount of the cash ... and the fair market value of the Broadcom Common Stock received in exchange ..., minus the holder’s adjusted tax basis in ... VMware Common Stock surrendered..., and
> (2) the amount of cash received for such share of VMware Common Stock.

We recognize gain, per lot, on the lessor of:
* `cash portion`
* `cash portion + FMV AVGO - VMW basis`

You'll recognize the cash unless your VMW basis was higher than the FMV of the AVGO received.



### Basis calculation - post-acquisition sale of AVGO

The concise version of future tax basis of RSUs, calculated per lot, is:
* basis prior to merger - cash received + gain recognized

Gain recognized is the lesser of (per Form 8937):
* cash received
* cash received + FMV AVGO received - basis prior to merger

That simplifies to the lesser of:
* basis prior to merger
* FMV AVGO received



### On Fair Market Value

[Yahoo Finance market data for the period in question](https://ca.finance.yahoo.com/quote/AVGO/history?period1=1700438400&period2=1700870400&interval=1d&filter=history&frequency=1d&includeAdjustedClose=true)

> Fair market value generally is the price at which property would change hands between a willing buyer and a willing seller, neither being under any compulsion to buy or sell and both having reasonable knowledge of the facts.

>  ... tax law does not specifically prescribe ... the fair market value ... for purposes of calculating any gain recognized ....
> One reasonable approach is ... the mean ... trading price on November 22, 2023, which is $979.50 .... Other approaches ... may be appropriate. _You should consult your tax advisor to determine what measure of fair market value is appropriate._

I have an [issue](https://github.com/hickeng/financial/issues/11) open to determine the knwoledge available to our hypothetical buyer/seller pair and add other FMV options to the dropdown in the spreadsheet.


### Fractional share sale

> A holder of VMware Common Stock who received cash in lieu of a fractional share ... will generally be treated as having received such fractional share and then as having received such cash in redemption of the fractional share.
> Gain or loss generally will be recognized based on the difference between the amount of cash in lieu of the fractional share and the tax basis allocated to such fractional share.

This details sequential steps of:
1. receive fractional share
2. sell fractional share

I'm interpreting that as needing to calculate the gain for the fractional share sale (step 2) using the new cost basis, post conversion. You'll have also seperately recognised gain on the conversion of the fraction (step 1).
If the fraction was attributed against an ESPP share this implies recognizing the ordinary income associated with the fraction given it's a sale.

> The amount paid for a fractional share of Broadcom Common Stock _was based on_ the closing price of Broadcom Common Stock as reported on the NASDAQ on November 21, 2023, which was $981.20.

eTrade did not use the value explicitly specified in f8937 for the fraction. I do not know what consequence "based on" has in this sentence. I've an [issue](https://github.com/hickeng/financial/issues/12) to determine handling for this.
