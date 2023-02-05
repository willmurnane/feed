# adsb.lol / feed


[adsb.lol](https://adsb.lol) is an open-source, community-driven ADS-B / UAT / MLAT feed aggregator.

We are always looking for new contributors. Our code is open source and we welcome pull requests ([See todo](https://adsb.lol/todo))

This includes the [infrastructure](https://github.com/adsblol/infra), [API](https://github.com/adsblol/api) and [history](httprs://github.com/adsblol/history) services.

The adsb.lol feed client is a toolkit that allows you to install, run and maintain a ADS-B / UAT / MLAT / ACARS / VDL2 feed client.

It is built with ease of use in mind. It is designed to be run on a Raspberry Pi, but can be run on any Linux Debian-like system.

## Quick Start
Run this on **as root** a fresh install of Raspberry Pi OS Lite or similar

```
bash <(curl -Ls https://raw.githubusercontent.com/adsblol/feed/main/bin/adsblol-init)
cd /opt/adsblol/
cp .env.example .env
nano .env
```

Then, edit the `.env` file to your liking.

```
adsblol-debug && adsblol-up
```
<http://IP:8080/> to confirm that readsb is working, <http://IP:8082/> to confirm that the adsblol multifeeder is working.

## Usage

By default, the client will feed to adsb.lol.

To see the current list of supported aggregators, see the [services.txt](services.txt) file.

The `adsblol` service supports feeding to multiple aggregators.

If you have an issue with the feed client, please [paste.ee](https://paste.ee) your error logs join our chat on [matrix](https://matrix.to/#/#adsblol:gatto.club) or [discord](https://adsb.lol/discord).

## Feeding to other aggregators

The `adsblol` service can feed to other aggregators.

To feed <adsb.one> and <theairtraffic.com>, two community aggregators we actively work with to share data, follow these steps.

Edit the .env file and ensure these lines look like this:

```
READSB_ADDITIONAL_NET_CONNECTOR=feed.adsb.one,64004,beast_reduce_out,feed.theairtraffic.com,30004,beast_reduce_out
ASDBLOL_ADDITIONAL_MLAT_CONFIG=feed.adsb.adsb.one,64006,39001;feed.theairtraffic.com,31090,39002
MLAT_MLATHUB_NET_CONNECTOR=adsblol,39000,beast_in,adsblol,39001,beast_in,adsblol,39002,beast_in
```

If you want to feed to other types / commercial aggregators, you will need to edit the `services.txt` file.

To do this, open the `services.txt` file and enable the aggregator by uncommenting it.

You may have to define further environment variables in the `.env` file.

Then, run `adsblol-gen` to generate a new cmdline.txt.

The cmdline.txt is used by the adsblol binaries to know what services to start.

Once you have done this, run `adsblol-up` to start the containers.

## Troubleshooting

Running `adsblol-debug` will tell you about common mistakes.

### Logs

- `adsblol-logs` - view logs
- `adsblol-logs -f` - view logs and follow
