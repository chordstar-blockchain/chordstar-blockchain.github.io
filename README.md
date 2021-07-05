# Chordstar Blockchain

## Block Description

### Version 0.1

A block is a `tar.gz` file named `chordstar-N` where `N` is an integer without leading zeros, representing
the block number from 1 up to the latest in order. There may be exactly one of each number and there must
be no breaks in the chain.

The archive consists of a `tar` archive named `files.tar` and a metadata file on `json` format named `meta.json`.
`files.tar` contains a top-level directory named `files`, which in turn contains all files included in this block.
Those files are supposed to be on `chordpro` format, but that is a soft requirement without validation. (TODO: really?)

The `metadata.json` is on a format examplified by:

    {
        "block_version": "0.1",
        "previous_block_sha512": "base",
        "toc": {
            "ChordStar.chopro": {
                "by": "cc6533a13dac39bf45abbb71ea64b648",
                "checksum_md5": "463a2e326b1cb953760f53f749e0cab5",
                "type": "new"
            }
        },
        "signatures": [
            "cc6533a13dac39bf45abbb71ea64b648"
        ],
        "pubkey_fingerprints_md5": {
            "cc6533a13dac39bf45abbb71ea64b648": "MFwwDQYJKoZIhvcNAQEBBQADSwAwSAJBANWZm8D7LmAfhFFHghOJXtl5lMu10Mu6zi4IP80Un8os0n1aHiXYh2KEi7/okd6l8jsoNDKbiy6bsJ8vV0wU2OsCAwEAAQ=="
        }
    }


* `block_version`: the current version
* `previous_block_sha512`: sha512 checksum of the previous block (`chordstar-N`) file
* `toc`: Table of contents, i.e a dictionary where each file name represents the key, with a dictionary as value containing
  * `by`: md5 fingerprint of the public key representing the author of this file
  * `checksum_md5`: md5 checksum of the file contents
  * `type`: One of `new`: new file, `change`: diff of an existing file
* 
* `pubkey_fingerprints_md5`: set of all `toc`/`by` values as keys and their base64 encoded public key (not the full PEM, but just the payload with eliminated linebreaks)
* `signatures`: list of md5 fingerprints used to sign this entire block
