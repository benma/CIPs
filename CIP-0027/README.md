---
CIP: 27
Title: CNFT Community Royalties Standard
Authors: Huth S0lo <john@digitalsyndicate.io>, TheRealAdamDean <adam@crypto2099.io>
Comments-URI: https://forum.cardano.org/t/cip-royalties/68599
Status: Draft
Type: Standards
Created: 2021-08-29
License: Apache-2.0
---

## Simple Summary

A community standard for royalties&#39; functionality, that does not require smart contracts to implement.

## Abstract

This proposed standard will allow for uniform royalties&#39; distributions across the secondary market space. It is easy to implement using metadata only, and does not require a smart contract.  However, it is scalable to allow for the usage of a downstream smart contract, as needed by the asset creator. It has been developed with input from Artano, BuffyBot, CNFT.io, Digital Syndicate, Fencemaker, MADinArt, NFT-Maker.io, Hydrun, Tokhun, and many more.

## Motivation

There is a significant interest within the Cardano Community for an implementation of royalties distribution when a Cardano Asset is resold on the secondary market. It has become a common theme to see and hear statements that the only thing stopping artists from adopting Cardano, is that they are waiting for an implementation of royalties.  At the present time, smart contracts do not create a simple mechanism to implement royalties.  By developing a community standard, we can resolve the immediate need for royalties, and create a path forward for a potential future iteration of smart contracts.

## Specification

A new tag of 777 is proposed for this implementation.  The community guidelines have been agreed as follows:
1) A brand new unused policy for implementation is required.
2) The royalties tags are to be written to an unnamed token, using the policy to be used for the intended Cardano Assets.
3) Only the first minted set of instructions will be honored.  Any future updates or rewrites will be ignored.  This prevents a Cardano Asset maker from changing the royalties at a future date.
4) Within this created asset will be the metadata for royalties distributions.  It will use a tag of 777, and then have two tags to identify the percentage of future sales requested as a royalty, and the payment address to forward those royalties to.  Those tags will be "rate" and "addr" respectively.
5) The "rate" key tag can be any floating point value from 0.0 to 1.0, to represent between 0 and 100 percent.  For example, a 12.5 percent royalty would be represented with "rate": "0.125".  Previous version 1.0 of this proposal used pct instead of rate.  Marketplaces to continue to honor legacy pct tag.
6) The "addr" key tag can be a string value, or an array.  It is to include a single payment address.  By allowing for an array, the payment address can exceed the per line 64 character limitation.  This payment address could be part of a smart contract, which should allow for greater flexibility of royalties distributions, controlled by the asset creator.
7) The royalty token must be minted prior to creating any assets off the policy.  All markets will be instructed to look only for the first minted asset on a policy, which would need to be the unnamed 777 token.

## Example JSON with string

{
	"777": {
		"rate": "0.2",
		"addr": "addr1v9nevxg9wunfck0gt7hpxuy0elnqygglme3u6l3nn5q5gnq5dc9un"
	}
}

## Example JSON with array

{
	"777": {
		"rate": "0.2",
		"addr": [
			"addr1q8g3dv6ptkgsafh7k5muggrvfde2szzmc2mqkcxpxn7c63l9znc9e3xa82h",
			"pf39scc37tcu9ggy0l89gy2f9r2lf7husfvu8wh"
		]
	}
}

## Process Flow
1) Create policy for planned assets.
2) Mint no name token with community standard royalties metadata.
3) Burn no name token to free up UTxO (recommended, but not required).
4) Mint planned assets using this same policy.

## Rationale

By creating a new tag for the distinct purpose of royalties distributions, Cardano Asset makers, and Marketplaces can uniformly apply royalties to assets with predictable results.  By creating the instructions on a single, no name token, all marketplaces will know the correct location of the royalties asset, without having to further locate it.  By enforcing the requirement of honoring only the first mint, cardano asset buyers and owners can predict the future resale value of the assets in their possession.  The solution is scalable to any desired royalty percentage.  It is easy to work with this new standard, and does not require an in depth understanding of smart contracts.

## Change Log

## Initial proposal - August 14th, 2021
## Revised proposal - August 28th, 2021
## Minor Revision - August 31st, 2011
## Minor Revision - September 27th, 2021
## Minor Revision - November 8th, 2021

Copyright

This CIP is licensed under [CC-BY-4.0](https://creativecommons.org/licenses/by/4.0/legalcode)
